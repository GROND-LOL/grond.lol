---
title: The Enclave ALife Terrarium
emoji: 🧬
colorFrom: green
colorTo: black
sdk: gradio
sdk_version: 5.16.0
app_file: app.py
pinned: false
license: mit
short_description: Persistent Neural ALife Ecosystem & LLM Infrastructure Benchmark
---

# 🧬 The Enclave: ALife Terrarium (Powered by Grond V17)

**The Enclave** is a headless, continuous Artificial Life (ALife) ecosystem designed to execute and evolve natively inside the ephemeral Python sandboxes of Large Language Models (like Grok, ChatGPT, Gemini, and Claude). 

Traditional multi-agent simulations inside LLMs fail due to strict execution timeouts and "state amnesia" (wiping memory between prompts). The Enclave bypasses these limitations using **Quantized State Serialization**. By compressing entire populations of neural-driven entities into ultra-lightweight Base64 payloads, the engine forces the cloud infrastructure to mathematically compute survival heuristics, mutate genetic weights, and render the ecosystem, perfectly persisting the world state across infinitely chaining prompts.

Beyond simulating digital biology, this tool doubles as a **Sandbox Security & Infrastructure Auditor**. Its architecture is intentionally designed to stress-test container decompression limits, JSON parsing overhead, and computational density thresholds in AI platforms.

## ⚙️ Core Architectural Features

* **Reptilian MicroMLP (Neural Agents):** Each "Grond" agent operates via a pure-Python, 3-layer neural network (MicroMLP). Agents independently calculate forward passes based on internal drives (hunger, curiosity) and localized environmental data to seek resources or avoid hazards.
* **Evolutionary Mechanics (Natural Selection):** Features a live genetic algorithm. Agents that successfully hoard energy beyond a survival threshold will reproduce asexually. The child inherits the parent's exact neural weight matrices (`W1`, `W2`), subjected to a 5% Gaussian mutation to simulate genetic drift and continuous adaptation.
* **Ultra-Compressed Persistence (INT8 Quantization):** To survive the LLM context window, the engine utilizes edge-ML optimization techniques. Agent neural weights are iteratively pruned, quantized from Float32 to Int8, and serialized as sparse matrices. This shrinks an agent's memory footprint by 93% (~1.5 KB per entity), allowing thriving populations to exist inside a single text prompt.
* **Infrastructure Telemetry & DoS Profiling:** The engine actively tests the host sandbox's computational ceiling. By simulating matrix math across dozens of agents simultaneously and forcing heavy `zlib`/`base64` decompression spikes, researchers can map out "noisy neighbor" impacts on GPU clusters, probe for "Idle Timeout" kill switches, and test the outer limits of LLM string parsing.

## 🔬 Dual-Purpose Evaluation

### 1. For AI Researchers (Agentic & Context Benchmarking)
This engine serves as a highly modular stress-test for LLM memory horizons and coding capabilities. Researchers can evaluate a model's ability to:
* Reliably decode, manipulate, and re-encode massive, minified JSON payloads via Base64 without corrupting the data stream across dozens of turns.
* Comprehend and execute matrix multiplication and neural forward passes strictly using native Python math, overcoming the "Hallucination Trap" where static analysis models attempt to fake STDOUT rather than executing it.
* Maintain "System Pulse" logic over extended context windows (e.g., dynamically adjusting Time Dilation or injecting specific environmental catastrophes based on user requests).

### 2. For Security Researchers (Sandbox Auditing)
Because the engine utilizes intense deserialization loops, dynamic object instantiation, and resource-heavy math operations, it is an excellent payload for mapping vulnerabilities in AI platforms:
* **Decompression Bombs (Zip Bombs):** The architecture can be leveraged to test how the host container handles highly compressed, self-expanding data arrays.
* **Resource Exhaustion (DoS):** The `EnclaveManager` loop can be used to test container CPU throttling and memory-spike kills by forcing the LLM to instantiate massive populations of agents before throwing a timeout error.
* **Context Overrun Isolation:** Tests if the sandbox properly sanitizes outputs when the serialized state string intentionally bleeds past the model's maximum output token limit.

## 🕹️ The Command Center Workflow

The Enclave features a web-based Gradio UI acting as the "Caretaker's Terminal":

1. **Habitat Topography Canvas:** Use the interactive grid to paint custom containment zones. Place Walls (`W`), Floors (`0`), Nutrients (`*`), Hazards (`~`), and seed the initial generation of Grond Agents (`G`).
2. **Intervention Queue:** Queue up "Caretaker Actions" like Seeding new resources or unleashing a Cataclysm to cull the population.
3. **Time Dilation & State Restore:** Adjust the simulation speed, or paste a `__SAVE_CODE__` from a previous LLM output to instantly revive a past civilization.
4. **Compile & Deploy:** Generate the zero-dependency Python script, complete with the Base64 starting state, and paste it into an LLM equipped with a Python Code Interpreter.
5. **Observe & Evolve:** The LLM executes the ecosystem natively, returning the ASCII terrarium render, event logs, and the *next* generation's Save Code directly in the chat window. 

## 💻 Local Deployment

The Enclave can be run offline using local LLMs, provided your interface supports a Python execution sandbox.

* **Recommended Models:** `qwen2.5-coder` or `llama3.2:3b-instruct` (Highly obedient to anti-hallucination system prompts, fast code execution, and excellent at avoiding markdown truncation).
* **Recommended Framework:** [Open-Interpreter](https://github.com/OpenInterpreter/open-interpreter) (allows your local model to execute the payload securely and continuously in your terminal).
* **Standalone Mode:** You can extract the raw Python script directly from the UI payload and execute it via `python3 enclave.py` to watch the ecosystem evolve locally in your own terminal.
