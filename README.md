# Pool Caustics

Real-time WebGL caustics simulation — the shimmering light patterns cast on a pool floor by sunlight refracting through moving water.

Two standalone HTML demos, no dependencies, no build step.

## Files

| File | Description |
|---|---|
| [caustics.html](caustics.html) | Full-featured demo with filmic tonemapping, surface sparkle, render quality control, and a timed title overlay |
| [caustics_mini.html](caustics_mini.html) | Lighter variant using a Voronoi caustic algorithm with wobbling grout lines |

## Usage

Open either file directly in a browser. WebGL 1 support is required (all modern desktop and mobile browsers qualify).

```
open caustics.html
# or serve locally:
npx serve .
```

## Controls

| Control | Effect |
|---|---|
| Water color | Base hue of the water and pool floor — pick from presets or use the color picker |
| Speed | Animation speed of the water surface |
| Caustics | Brightness of the refracted light patterns |
| Rainbow | Chromatic dispersion / spectral fringing on caustic edges |
| Tile size | Scale of the pool floor tiles |
| Ripple | Refraction / distortion strength of the surface waves |
| Quality | *(caustics.html only)* Render resolution multiplier — lower for performance |

Press **H** to hide/show the control panel.

## How it works

### caustics.html

Uses an iterative wave-folding technique: four nested sinusoidal passes accumulate phase offsets that create bright convergence filaments — the way real caustics form when parallel light rays are concentrated by a curved refracting surface. The pool floor is procedurally tiled with per-channel chromatic dispersion applied to fake light wavelength separation. A filmic Uchimura-style tonemap and a subtle grain pass prevent the output from looking too synthetic.

### caustics_mini.html

Uses a Voronoi cell approach: animated cell centers produce thin bright ridges at cell boundaries, layered at two scales and speeds. Grout lines on the pool floor wobble with the water surface, and chromatic aberration is derived from the caustic edge gradient.

Both shaders share the same surface ripple model — layered fractional Brownian motion (fBm) sampled as a finite-difference gradient to compute a refraction offset vector.

## Browser requirements

- WebGL 1 (`OES_standard_derivatives` not required)
- `highp float` precision fragment shaders (universally available on desktop; most mobile)
