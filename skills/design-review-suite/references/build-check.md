# BUILD-CHECK: the 15 lines, run by command

Source of the 15 lines: `standards.md` section 6. This file is only the how.

Rule: a line reports PASS or FAIL only when a command produced the value. A line you could
not run reports `SKIP, reason`. Never report PASS from reading the code.

## A. Rendered-page checks (lines 1 to 9, 10, 11, 15)

Serve the page locally first, then run the probe below in the page context. Any of these
delivery routes works, pick what the environment has:

- A browser automation tool that evaluates JavaScript in the page.
- `node --input-type=module` with Playwright or Puppeteer installed, `page.evaluate(probe)`.
- Paste into the browser console and copy the JSON out.
- No package installs available: inline the probe into a copy of the page inside a
  `<script>` that sets `document.title = JSON.stringify(probe())`, then run
  `chrome-headless-shell --headless --window-size=W,H --virtual-time-budget=1500
  --dump-dom file://<page>` and parse the title. Verified working 2026-08-28.

Save the probe to `build-check.js` and evaluate it. It returns one JSON object.

```js
() => {
  const lum = colour => {                     // relative luminance from "rgb(r, g, b)"
    const f = c => { c /= 255; return c <= 0.03928 ? c / 12.92 : ((c + 0.055) / 1.055) ** 2.4; };
    const [r, g, b] = colour.match(/\d+/g).map(Number);
    return 0.2126 * f(r) + 0.7152 * f(g) + 0.0722 * f(b);
  };
  const ratio = (fg, bg) => { const a = lum(fg), b = lum(bg);
    return (Math.max(a, b) + 0.05) / (Math.min(a, b) + 0.05); };
  const bgOf = el => { for (let n = el; n; n = n.parentElement) { const c = getComputedStyle(n).backgroundColor;
      if (c && !/rgba\(0, 0, 0, 0\)|transparent/.test(c)) return c; } return 'rgb(255, 255, 255)'; };
  const all = [...document.querySelectorAll('*')];
  const text = all.filter(e => [...e.childNodes].some(n => n.nodeType === 3 && n.textContent.trim()));
  const contrast = text.map(e => { const s = getComputedStyle(e);
    const px = parseFloat(s.fontSize), bold = parseInt(s.fontWeight, 10) >= 700;
    const large = px >= 24 || (px >= 18.66 && bold);
    return { sel: e.tagName.toLowerCase() + (e.className ? '.' + String(e.className).split(' ')[0] : ''),
             px, large, r: +ratio(s.color, bgOf(e)).toFixed(2), need: large ? 3 : 4.5 }; })
    .filter(x => x.r < x.need);
  const targets = [...document.querySelectorAll('a,button,input,select,textarea,[role=button],[tabindex]')]
    .map(e => { const b = e.getBoundingClientRect();
      return { sel: e.tagName.toLowerCase(), w: Math.round(b.width), h: Math.round(b.height) }; })
    .filter(t => t.w > 0 && (t.w < 24 || t.h < 24));
  const fonts = [...new Set(all.map(e => getComputedStyle(e).fontFamily.split(',')[0].replace(/["']/g, '').trim()))];
  const shadows = all.filter(e => { const s = getComputedStyle(e);
    return (s.boxShadow && s.boxShadow !== 'none') || /gradient/.test(s.backgroundImage); }).length;
  const body = document.body.innerText;
  return {
    contrastFailures: contrast.slice(0, 20), contrastFailureCount: contrast.length,
    targetFailures: targets.slice(0, 20), targetFailureCount: targets.length,
    fontFamilies: fonts, fontFamilyCount: fonts.length,
    tabularNums: all.filter(e => /tabular-nums/.test(getComputedStyle(e).fontVariantNumeric)).length,
    shadowOrGradientCount: shadows,
    bannedGlyphs: (body.match(/[—–→←⇒]/g) || []).length,
    emoji: (body.match(/\p{Extended_Pictographic}/gu) || []).length,
    welcomeCopy: /\bwelcome\b/i.test(body),
    scrollHeight: document.documentElement.scrollHeight,
    clientHeight: document.documentElement.clientHeight,
    horizontalScroll: document.documentElement.scrollWidth > document.documentElement.clientWidth
  };
}
```

Reflow, line 8: set the viewport to 320 by 800 CSS px, re-run, and read `horizontalScroll`.
Viewport fit, line 15: set the viewport to the size the user stated, re-run, and compare
`scrollHeight` to `clientHeight`.

Focus, lines 6 and 7: no reliable static probe. Tab through every stop with the page
visible, screenshot the focused state, and report the stop that fails. Report
`SKIP, not run` rather than guessing.

## B. Source checks (lines 12, 13, 14), no browser needed

Run from the UI source directory. Adjust the glob to the project.

```bash
# 12. Banned glyphs in UI copy: em dash, en dash, arrows
grep -rnP '[\x{2014}\x{2013}\x{2192}\x{2190}\x{21d2}]' --include='*.tsx' --include='*.jsx' \
  --include='*.html' --include='*.vue' --include='*.svelte' . | grep -v node_modules

# 13. Emoji, "Welcome", hero heading
grep -rnP '\p{Extended_Pictographic}' --include='*.tsx' --include='*.html' . | grep -v node_modules
grep -rniE '>[^<]*\bwelcome\b' --include='*.tsx' --include='*.html' . | grep -v node_modules

# 14. Gradients and shadows
grep -rnE 'box-shadow|boxShadow|linear-gradient|radial-gradient|shadow-(sm|md|lg|xl)' \
  --include='*.css' --include='*.tsx' --include='*.html' . | grep -v node_modules
```

Lines 12, 13, and 14 are taste lines. When `local-context.md` is absent they report
`SKIP, no local taste file` rather than FAIL.

## C. Output shape

One line per checklist item, in checklist order, nothing else before the verdict.

```
BUILD-CHECK <target> at <viewport>
 1 PASS  body contrast 4.5:1          min measured 7.31:1 over 84 text nodes
 2 PASS  large text contrast 3:1      min measured 5.02:1 over 6 nodes
 4 FAIL  target size 24 CSS px        button.close measured 18x18, required 24x24
 6 SKIP  focus ring visible           not run, no interactive session
...
VERDICT: SHIP or BLOCK, n FAIL, n SKIP
```

A single FAIL blocks. A SKIP does not block but must be named in the verdict line, so the
reader knows what was never checked.
