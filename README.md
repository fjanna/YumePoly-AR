# YumePoly-AR

**Everyone Can Be an Artist**

An interactive prototype for exploring a 3D creation, previewing it in augmented reality (AR), and making a more informed decision about 3D printing.

**[Open the live demo](https://fjanna.github.io/YumePoly-AR/)** · **[View the source code](https://github.com/fjanna/YumePoly-AR)**

> **Prototype status:** The current demo starts with a pre-generated capybara GLB model. Text-to-3D generation, real mesh analysis, live AI tutoring, and actual 3D printing are **not yet implemented**. The printability report and tutor messages use illustrative, predefined content.

## 1. Project concept

YumePoly explores a beginner-friendly path from a creative idea to a physical object:

**Text prompt → 3D model → 3D/AR preview → printability guidance → 3D printing**

The longer-term concept is to help non-experts see, evaluate, and refine AI-generated objects before committing to a print. The current prototype focuses on the **3D/AR preview and decision-support** portion of that experience.

## 2. Current features

| Feature | Current status | Notes |
| --- | --- | --- |
| Interactive 3D preview | Implemented | Rotate and zoom the bundled capybara model |
| AR preview | Implemented with device-dependent availability | Uses the browser-based \`<model-viewer>\` AR modes |
| Print-height selection | Implemented | 5 cm, 10 cm, or 15 cm; scales the displayed model |
| Printability report | **Simulated** | Prewritten observations about thin features, details, and material/time |
| AI Tutor interface | **Simulated** | Predefined guidance, alternative sizes, and educational explanations |
| Design confirmation | Demo-only | Shows a confirmation state; does not save or export a design |
| Text-to-3D generation | Not implemented | No text prompt, generation API, or generation backend |
| Automated mesh validation | Not implemented | No actual geometric printability computation |
| STL / 3MF export | Not implemented | No printable file is produced |
| Printer integration | Not implemented | Nothing is sent to a printer |

### Demo walkthrough

1. **Explore:** Rotate or zoom the capybara in the 3D preview.
2. **Choose a size:** Select a target height of **5, 10, or 15 cm**.
3. **View in AR:** On a compatible mobile browser, select **View in AR** to attempt an AR placement.
4. **Check printability:** Click **Check Printability** to show a *simulated* report for the selected size.
5. **Review tutor guidance:** Try a suggested size, keep the current size, or select **Learn More**.
6. **Confirm:** Click **Confirm My Design** to complete the demonstration flow. This does **not** generate an STL, place an order, or start a print.

## 3. Technology

The prototype is a **static, client-side webpage**:

- **HTML, CSS, and vanilla JavaScript** for the UI and interaction logic.
- **[Google model-viewer](https://modelviewer.dev/)** (loaded from a CDN; version 3.5.0 in the current source) for 3D rendering and device-supported AR modes.
- **GLB / glTF** as the bundled 3D model format.
- **Google Fonts** (Zen Maru Gothic) for typography.
- **GitHub Pages** for hosting the static demo over HTTPS.

There is **no backend, database, model-generation service, LLM API, or printing service** connected to the current implementation.

## 4. Repository structure

~~~text
YumePoly-AR/
├── index.html          # UI, style, JavaScript, and demo logic
├── cute-capybara.glb   # Bundled 3D sample model
└── README.md           # This documentation
~~~

The sample model is credited in the demo to **Numan Amri Maliky**.

## 5. Run locally

You do not need a build tool or package manager.

1. Clone the repository or download its files.
2. Keep \`index.html\` and \`cute-capybara.glb\` in the **same directory**.
3. In a terminal, navigate to that directory and start a local HTTP server:

~~~bash
python3 -m http.server 8000
~~~

4. Open **http://localhost:8000/** in your browser.

Do **not** open the HTML through a \`file://\` URL. Browser restrictions can prevent the GLB from loading correctly.

### Requirements

- A modern browser with WebGL support for the 3D preview.
- An internet connection to retrieve the \`model-viewer\` library and Google Fonts from their CDNs.
- A supported mobile device/browser and HTTPS for AR functionality. **AR availability varies** by platform, browser, and device; a working 3D preview does not guarantee working AR.

For testing on a phone, use the [GitHub Pages demo](https://fjanna.github.io/YumePoly-AR/) rather than \`localhost\` on your computer.

## 6. How the demo works

### Model and scale

The page loads \`cute-capybara.glb\` into the \`<model-viewer>\` element. Selecting a print height changes the visual scale applied to that model.

The current source uses a **fixed reference height** for this particular GLB. If you replace the model, update the filename **and the reference height** (or implement reliable model-bound measurement) before relying on the displayed centimetre values.

### Printability guidance

The report is selected from hard-coded JavaScript data for the three available sizes. It illustrates the kinds of trade-offs a future printability system could explain:

- Thin walls and fragile details at smaller scales.
- Loss of small surface details.
- Material and print-time trade-offs at larger scales.

**These are not measured properties of the supplied mesh.** The labels, ratings, and explanations should not be used to determine whether a real print will succeed.

### Tutor

The **AI Tutor** currently displays static text and predefined actions. It does not call an LLM, remember a conversation, or perform new analysis.

## 7. Known limitations and troubleshooting

- **Model not visible:** Check that \`cute-capybara.glb\` is beside \`index.html\` and opens from the deployed site. Inspect the browser DevTools **Console** and **Network** panels for load or parsing errors.
- **AR button unavailable:** Verify HTTPS, device/browser compatibility, and platform-specific AR requirements. Desktop browsers usually provide only the 3D preview.
- **Changed model behaves incorrectly:** The fixed reference height and the sample-specific guidance must be revisited for every replacement GLB.
- **Printability results look repetitive:** They are intentionally predefined for demonstration and do not reflect real mesh analysis.
- **Confirmation is not an export:** The page does not generate STL/3MF or communicate with a printer.

## 8. Proposed next steps

These are **ideas for future development**, not current features:

1. **Text-to-3D integration:** Add a prompt UI, generation service, progress state, and a way to load newly generated models.
2. **Reliable model handling:** Validate uploaded/generated GLBs, handle loading errors, and compute scale from actual model geometry.
3. **Printability analysis:** Investigate mesh integrity, minimum wall thickness, overhangs, and size-dependent printing constraints.
4. **Context-aware tutoring:** Replace static guidance with model-grounded explanations, with safeguards against unsupported claims.
5. **Production workflow:** Explore printable-file preparation, slicer integration, and export rather than implying that preview alone makes a model print-ready.
6. **Cross-device UX:** Test AR behavior and performance on Android and iOS.

## 9. Collaboration workflow

For changes to the demo:

1. Create a short-lived branch, e.g. \`feature/text-to-3d\`, \`feature/ar-ux\`, or \`fix/model-loading\`.
2. Make one focused change and test it locally.
3. Commit with a descriptive message such as \`fix: handle GLB loading failures\` or \`docs: clarify prototype limitations\`.
4. Open a **pull request** targeting \`main\`. Describe what changed and how it was tested.
5. Review and merge. GitHub Pages publishes from \`main\`.

Do not commit API keys, tokens, or other secrets to this repository. Any future text-to-3D API integration needs an appropriate server-side secret-management strategy, not an exposed key in client-side JavaScript.

## 10. Model attribution and reuse

The included \`cute-capybara.glb\` is credited to **Numan Amri Maliky** in the demo. Before distributing or reusing the model outside this collaboration, confirm its licensing and attribution requirements with the creator.

**License:** No open-source license has been assigned to this repository at present. Public visibility on GitHub does not by itself grant permission to reuse the code or model.
