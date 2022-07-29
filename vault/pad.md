---
id: wfpnlg17mot2pbykl0s89oc
title: Scratchpad
desc: ''
updated: 1659053144454
created: 1659050776336
---
$∑_{t=0}^n k(x_{t-1} + d)$

1. $x_1 = (x_0 + d)k = dk + x_0$
2. $x_2 = (x_1 + d)k = (dk + x_0)k = dk^2 + x_0k$
3. $x_3 = (x_2 + d)k = (dk^2 + x_0k + d)k = dk^3 + x_0k^2 + dk$
4. $x_4 = (x_3 + d)k = (dk^3 + x_0k^2 + dk + d)k = dk^4 + x_0k^3 + dk^2 + dk$

$∑_{t=0}^{n-2}dk^t = d∑_{t=0}^{n-2}k^t$

$x_n = dk^n + x_0^{n-1} + (d∑_{t=0}^{n-2}k^t\ \text{if}\ t > 2,\ \text{else}\ 0)$