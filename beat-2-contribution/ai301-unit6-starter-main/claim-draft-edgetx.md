Hi, I'd like to take on the remaining radio side of this, since the Companion side was resolved in #1078.

So far I've read `radio/src/curves.cpp` on `main`: `applyCustomCurve()` sends an undefined curve (all points zero, so `isCurveUsed()` is false) straight to `intpol()`, which returns 0. That matches @raphaelcoeffic's note that only unused curves read as Y = 0. My next step is reproducing it in the radio simulator by selecting a never-defined curve on a mix, and I'll post what I find here before changing any code.

Following the later exchange between @gagarinlg and @pfeerick, which approach would you prefer: have `applyCustomCurve()` return `x` when `isCurveUsed()` is false (Y = X, as this issue proposes), or limit the curve selection popup to configured curves?

*(Note: prepared with AI assistance via Claude Code; I'll review and verify everything I post.)*
