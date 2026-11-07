# YumePoly-AR

An interactive demo of YumePoly's AR preview and 3D printing decision-support features.

**Live Demo:** https://fjanna.github.io/YumePoly-AR/

## Features

- **3D Preview:** Rotate and zoom a pre-generated 3D model.
- **AR Preview:** Place the model in a real-world environment using a compatible mobile device.
- **Size Selection:** Choose a print height of 5, 10, or 15 cm and preview the model at the selected scale.
- **Printability Check:** Explore potential printing considerations, including thin walls, small details, and material usage.
- **AI Tutor:** Receive educational explanations and suggestions for adjusting the print size.

**Current limitations:** The AR preview and size selection are functional, but the printability analysis and AI Tutor use simulated results to demonstrate the concept. Text-to-3D generation and actual 3D printing are not yet integrated.

## Device Compatibility

- **PC:** Interactive 3D preview is available, but AR is not supported.
- **Android:** Chrome works best for AR. Some devices may require Google Play Services for AR.
- **iPhone:** Safari works best. Move your phone around to help detect a flat surface, especially when placing the model on a table.

AR availability may vary depending on the device and browser.

## Technical Details

The demo is built using HTML, CSS, and JavaScript, with Google's `model-viewer` library for 3D rendering and AR.

The current version uses a pre-generated capybara model (`cute-capybara.glb`).

### Project Files

```text
YumePoly-AR/
├── index.html
├── cute-capybara.glb
└── README.md
```

### Local Testing

Run a local server in the project directory:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000 in your browser.

## Credits

Developed for YumePoly, Programming Boot Camp (PBC), Institute of Science Tokyo.

- **AR Demo Development:** Jie Feng
- **3D Sample Model:** Numan Amri Maliky
