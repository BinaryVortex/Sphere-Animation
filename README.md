# Sphere Animation

![Screenshot](./Screenshot%202024-08-23%20084647.png)

A minimal, GPU-accelerated sphere animation built with Three.js and custom GLSL shaders. The project demonstrates how to use BufferGeometry, per-vertex attributes, and simple edge-aware fragment shading to create a stylized wireframe-like sphere.

## Demo

Open `index.html` in a modern browser (Chrome, Firefox, Edge, Safari) to see the animation. For best results serve the folder over HTTP (some browsers restrict loading local files into WebGL):

- Python 3: `python -m http.server 8000`
- Node (http-server): `npx http-server`

Then open `http://localhost:8000` in your browser.

## Files

- `index.html` – Main demo. Creates the scene, sphere geometry, and custom shaders.
- `style.css` – Minimal page styling.
- `Screenshot 2024-08-23 084647.png` – Example screenshot used in this README.

## How it works (short)

- A `SphereBufferGeometry` is created and converted to non-indexed form so each triangle can have its own vertex attributes.
- A custom `center` attribute is added and repeated in a 3-vector pattern per triangle to let the fragment shader compute an "edge factor" for each triangle.
- The fragment shader uses GLSL's `fwidth` and `smoothstep` to build a soft edge mask and discard fragments beyond a threshold, producing a stylized outline effect.
- The material enables derivative extensions (`material.extensions.derivatives = true`) so `fwidth` works in the shader.

## Customization

- Change sphere size: edit `var size = 150;` in `index.html`.
- Increase detail: increase segments in `new THREE.SphereBufferGeometry(size, 16, 8)` (e.g. 32, 16).
- Line thickness: tweak the `lineWidth` uniform value in `index.html` (default is `3`).
- Background color: change `scene.background = new THREE.Color(0x1d233b);`.

## Troubleshooting

- Blank screen: ensure WebGL is enabled and supported by your browser. Check the developer console for errors.
- If the screenshot doesn't appear in the README on GitHub, confirm the image file is present at the repository root and the filename matches exactly (including spaces).

## Credits

- Built using Three.js (r89 via CDN in `index.html`).

If you'd like, I can also add a small live demo link using GitHub Pages and update the Three.js version to a newer release. What would you prefer?