# 🔬 GROND ENVIRONMENT: Explicit Simulation Framework (v2.0)

**Grond** is a headless, stateless 2.5D Raycasting environment designed to execute entirely inside the Python code-interpreter sandboxes of Large Language Models (like Grok, ChatGPT, or Claude). 

Because LLM execution containers suffer from "state amnesia" (they wipe memory between prompts) and strict execution timeouts, traditional Interactive World Simulation inside an LLM is extremely difficult. Most research attempts to solve this via *Implicit Simulation*—forcing neural networks to hallucinate frame states (e.g., GameNGen, Oasis).

The Grond Environment solves this via **Explicit Simulation**. It leverages a deterministic "Command Tape" architecture alongside a robust 2D matrix rendering pipeline to force the cloud infrastructure to mathematically prove the physical state on every execution. This generates un-hallucinated 3D ASCII renders of exact spatial topography without falling victim to terminal wrapping bugs.

## ⚙️ Core Architectural Features

* **Stateless Command Tape:** Bypasses LLM container amnesia by compiling all sequential agent inputs (`W, S, B, L, R, X`) into an execution array. On every prompt, the engine reconstructs the entire spatial history from `t=0` in milliseconds.
* **Stable 2D Matrix Rendering:** Replaces volatile C-level memory buffers with a native nested Python list structure. This entirely prevents "stride desync" (the funhouse mirror effect) across different cloud terminal emulators, ensuring perfect geometric stability. 
* **Infrastructure Awareness:** Dynamically profiles the sandbox's `os.cpu_count()` to scale rendering resolution, and hashes the container's `HOSTNAME` to inject execution-specific environmental entropy into the simulation.
* **Temporal Management:** Actively monitors `time.perf_counter()`. If the LLM sandbox approaches a 25-second timeout, the engine forces an immediate early render to save the state. Additionally, it implements "Temporal Integrity Decay," simulating continuous system drain.
* **Continuous Collision Detection (CCD):** Implements sub-cell micro-stepping to prevent fast-moving agents from tunneling through collision boundaries.
* **Fast Heuristics:** Replaces heavy `math.sqrt()` Euclidean distance checks with optimized squared-distance (`dist_sq`) thresholds for pathfinding, hitscan interactions, and trigger volumes.
* **Structured Telemetry:** Outputs a rich combat log and a strict JSON state dictionary (tracking coordinates, integrity, and resources). This is specifically formatted for LLM attention mechanisms, acting as a flawless spatial reasoning benchmark.

## 🕹️ The Evaluation Loop

You evaluate an agent by "correspondence." You do not move in real-time; you program a sequence of moves, send them to the LLM, and await the visual and structural snapshot.

1. **Design:** Use the Topology Architect (web UI) to paint your grid. Place the Agent (`A`), Obstacles (`O`), Logic Gates (`B`), Modifiers (`M`, `C`), and the Terminal Objective (`T`). Includes a default "Evaluation Track" designed as a Hub-and-Spoke tutorial. 
2. **Plot:** Use your keyboard or the UI controls to chart your path in the Real-Time Trajectory Preview.
3. **Generate:** Click `⚙️ GENERATE VALIDATION PAYLOAD` to compile your map and sequence into a single, zero-dependency Python script.
4. **Execute:** Paste the generated markdown block into an LLM equipped with a Python Code Interpreter.
5. **Analyze:** The LLM will execute the script natively and return a Spatial Topography Render (First-Person), an Orthogonal Projection (Minimap), and JSON Telemetry.
6. **Iterate:** Read the telemetry, add more moves to your queue in the web UI (do **not** clear the queue unless you want to reset to spawn!), and generate the next payload.

## 🔬 For AI Researchers

The Grond Environment serves as a highly modular stress-test for autonomous agents. 
By prompting an LLM to generate its own "Command Tapes" and evaluating the resulting JSON telemetry, researchers can benchmark an agent's spatial reasoning, object permanence, resource management, and ability to navigate deterministic physical constraints without the hallucination issues present in text-only environments.

## 💻 Local Deployment

Grond can be run entirely offline using local LLMs. However, your local interface **must** support a Python execution sandbox.

* **Recommended Models:** `qwen2.5:3b-instruct` or `llama3.2:3b-instruct` (Highly obedient to anti-hallucination system prompts, easily fits in 4GB VRAM).
* **Recommended Framework:** [Open-Interpreter](https://github.com/OpenInterpreter/open-interpreter) (allows your local model to execute the payload securely in your terminal).

## ⚠️ Anti-Simulation Override

LLMs will occasionally try to "guess" or hallucinate the ASCII output instead of actually running the code. The Grond payload includes a strict `[STRICT EXECUTION DIRECTIVE]` prompt that forces the model to use its Python tool and return the exact `stdout`. If your render looks jagged or the minimap loses its orthogonal geometry, prompt the LLM to *run the code natively*.
