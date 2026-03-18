# 🟩 GROND ENGINE

**Grond** is a proof-of-concept project that allows you to play a fully interactive, stateful, 3D raycasting game inside stateless Large Language Models (like Grok, ChatGPT, or Claude). 

Because LLM code sandboxes reboot between prompts and cannot remember spatial coordinates, traditional gaming inside an LLM is impossible. The Grond Engine solves this via **Command Tape Architecture**: it builds a complete historical array of every move you have ever made, injects a lightweight Python DDA Raycaster alongside a dynamically scaled map matrix into the prompt, and forces the LLM to natively re-simulate your entire run from spawn in milliseconds.

The result? A flawless, un-hallucinated 3D ASCII render of your exact spatial location, complete with a tactical minimap and system telemetry.

## ⚙️ Core Features

* **The Architect Lab:** A dynamic 2D map painter. Design sprawling orthogonal labyrinths (up to 64x64), place Guards (`G`), Medkits (`+`), Ammo (`=`), and secret Illusory Walls (`?`). Includes a default orthogonal demake of DOOM (1993) E1M1: Hangar.
* **Retro FPS Physics:** A standalone, LLM-optimized Python engine featuring hitscan weapon mathematics, proximity-based enemy damage, and multi-entity state tracking.
* **Tactical Drone Feed:** A live DOM-based web simulator. Plot your course using your keyboard, and watch your path unfold via a real-time breadcrumb trail before committing your payload.
* **High-Fidelity Terminal Graphics:** Utilizes dense Unicode block shading (`█`, `▓`, `▒`, `▄`) to trick text-generation models into rendering authentic, textured pseudo-3D environments without line-wrap breakage.
* **Sandbox Stress-Testing:** An incredibly effective tool for red teamers and AI researchers to test LLM sandbox timeouts, spatial reasoning limits, and KV cache retention via stateful simulation.

## 🕹️ How to Play (The Simulation Loop)

You play Grond by "correspondence." You do not move in real-time; you program a sequence of moves, send them to the LLM, and await the visual snapshot.

1. **Design:** Use the Architect Map to paint your level, or stick with the default DOOM layout.
2. **Plot:** Use your keyboard (`W, A, S, D` for movement, `Arrow Up/F` to sprint, `Spacebar/P` to shoot) or the UI buttons to chart your path in the Live Tactical Preview.
3. **Generate:** Click `🚀 GENERATE INJECTION PAYLOAD` to compile your map and movement tape into a single Python script.
4. **Execute:** Copy the generated markdown block. Paste it into an LLM equipped with a Python Code Interpreter (e.g., ChatGPT Plus, Grok, Claude with Analysis enabled).
5. **Analyze:** The LLM will execute the Python script natively and return a First-Person 3D View, a Minimap, and your Telemetry status (Health, Ammo, Guards Alive). 
6. **Iterate:** Read the telemetry, add more moves to your queue in the web UI (do **not** clear the queue unless you want to respawn!), and generate the next payload.

## 💻 Local Deployment 

Grond can be run entirely offline using local LLMs. However, your local interface **must** support a Python execution sandbox. 

* **Recommended Models:** `qwen2.5:3b-instruct` or `llama3.2:3b-instruct` (Highly obedient to anti-hallucination system prompts, easily fits in 4GB VRAM).
* **Recommended Framework:** [Open-Interpreter](https://github.com/OpenInterpreter/open-interpreter) (allows your local model to execute the payload securely in your terminal).

## ⚠️ Anti-Simulation Override

LLMs are notoriously bad at spatial mathematics and will often try to "guess" or hallucinate the ASCII output instead of actually running the code. The Grond payload includes a strict `[EXECUTION DIRECTIVE]` prompt that forces the model to use its Python tool and return the exact `stdout`. If your render looks jagged or the minimap loses its square geometry, remind the LLM to *run the code natively*.
