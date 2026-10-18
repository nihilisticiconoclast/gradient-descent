# gradient-descent

Gradient descent from first principles: a straight line fitted to five points, shown
three ways at once.

- **The line** — the data, the current fitted line, and each residual as a dashed miss.
- **The valley** — a contour map of the loss over every possible slope `m` and
  intercept `c`, with the route the descent has taken and an arrow pointing downhill
  (`−∇L`). Amber marks high ground; the cross marks the exact least-squares minimum.
- **The equations** — prediction, residuals, loss, both partial derivatives and both
  update steps, with the current epoch's numbers substituted in, so each line of
  algebra can be checked by hand.

Step through one epoch at a time with **+1 epoch**, or press **Play**. The whole run is
computed once on load; the controls only choose which moment to show.

## The idea

The loss is the average squared miss between the line's predictions and the known
answers. Because every pair `(m, c)` has a loss, the loss is a surface, and the best line
sits at its lowest point, where both partial derivatives are zero:

```
L(m, c)  = (1/n) Σ (yᵢ − m·xᵢ − c)²
∂L/∂m    = −(2/n) Σ xᵢ (yᵢ − ŷᵢ)
∂L/∂c    = −(2/n) Σ (yᵢ − ŷᵢ)
m ← m − η ∂L/∂m,   c ← c − η ∂L/∂c
```

Gradient descent does not solve for that point. It measures the slope where it stands
and steps against it, repeatedly. As the ground flattens the gradients shrink, so the
steps get shorter.

## What is idealised

The five points are invented, chosen so the run starts from a flat line at `c = 1.25`
with a loss near 0.59. The learning rate is fixed at `η = 0.01` and every update uses
all the data (full-batch descent). After 500 epochs the route has not quite reached the
minimum: the valley floor is long and shallow, so progress along it is slow at this
learning rate. A straight-line least-squares loss is a single bowl; neural-network loss
surfaces are not.

The page itself explains all of this in more detail below the instrument.

## Running it

It is one static file, `index.html`, with no build step. Open it in a browser, or serve
it with GitHub Pages (Settings → Pages → deploy from the `main` branch, root folder).

It needs network access at load time for:

- the [Tunnel](https://github.com/nihilisticiconoclast/cuddly-lamp) house style —
  `tokens.css` and `tunnel-figure.js`, linked from jsDelivr at `@main`, not copied in,
  so updates to the design system reach this page automatically;
- [KaTeX](https://katex.org/) 0.16.9 from cdnjs, for the equations;
- the Fraunces, Public Sans and IBM Plex Mono fonts from Google Fonts.
