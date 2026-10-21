# This AI Costs Nothing

An interactive web experiment demonstrating zero-cost, client-side AI inference using browser tab memory. 

## Overview

Traditional AI web applications rely on cloud GPUs to process user prompts, creating a continuous server cost deficit for developers offering free tools. This project bypasses server infrastructure entirely by streaming quantized Small Language Models (SLMs) directly into the user's browser memory (RAM) via WebAssembly (WASM) and ONNX Runtime, or by tapping into Chrome's native on-device model.

Once the model weights are cached in the tab's memory, all matrix math and text generation occur locally on the client's CPU/GPU. The server bill remains $0.00 regardless of traffic, and prompts never leave the user's device.

## Features

- **Visual Architecture Breakdown**: Interactive diagrams and charts illustrating how browser tabs allocate memory across the DOM, JavaScript heap, and WebAssembly buffers.
- **Composite Tab RAM Telemetry**: A real-time memory monitor that estimates total tab consumption by combining the Chromium renderer baseline, live V8 JS heap (`performance.memory`), and allocated WASM model buffers.
- **In-Tab WASM Inference (Transformers.js)**: Streams quantized instruction-tuned T5 models from Hugging Face directly into the browser tab with selectable parameter sizes:
  - `Xenova/LaMini-Flan-T5-77M` (~85 MB RAM)
  - `Xenova/LaMini-Flan-T5-248M` (~250 MB RAM)
  - `Xenova/LaMini-Flan-T5-783M` (~780 MB RAM)
- **Built-in Browser AI (`window.ai`)**: Supports Chrome's native Prompt API (Gemini Nano) for zero-download local execution on supported hardware.
- **Offline Capability**: Once the model finishes streaming into memory, the chat interface functions completely offline.

## Getting Started

This project is built as a single, self-contained HTML file with no build step or backend dependencies.

### Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/Snorkel-Boy/this-ai-costs-nothing.git
   cd this-ai-costs-nothing
   ```

2. Start any local static server (required for ES modules):
   ```bash
   # Using Python
   python3 -m http.server 8000

   # Or using Node.js
   npx serve .
   ```

3. Open `http://localhost:8000` in your browser.

### Optional: Enabling Chrome Built-In AI (Engine B)

Engine A (Transformers.js) works out of the box in any modern browser. To test Engine B (`window.ai`), use Google Chrome and enable the experimental Prompt API:

1. Navigate to `chrome://flags/#prompt-api-for-gemini-nano` and set it to **Enabled**.
2. Relaunch Chrome.
3. Verify the background model download status at `chrome://on-device-internals`.

## Tech Stack

- **HTML5 & Vanilla JavaScript (ES Modules)**
- **Tailwind CSS** (Styling)
- **Transformers.js (`@xenova/transformers`)** (Client-side ONNX/WASM inference)
- **Chrome Prompt API (`window.ai`)** (Native browser inference)

## Author

By [Lucas Mathai](https://github.com/Snorkel-Boy)