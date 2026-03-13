[**Access the full dataset and data viewer on Hugging Face here.**](https://huggingface.co/datasets/yatin-superintelligence/Creative-Professionals-Agentic-Tasks-1M)

# Creative Professionals Agentic Tasks (1M)

## Abstract

A massive-scale, high-fidelity synthetic task dataset featuring **1,070,917** agentic command operations across 36 creative, technical, and engineering software environments. This dataset is engineered exclusively to stress-test, evaluate, and fine-tune multimodal AI for Agent Environment operation, complex software interaction, and multi-step reasoning within deep software infrastructures.

<img src="Creative Professional Robot.jpg" alt="Creative Professional Robot" width="100%"/>

## Infrastructure Architecture & Scale

The Creative Professionals Agentic Tasks dataset is built at a scale designed for core-level agent training, focusing on the semantic gap between high-level user intent and absolute tool-level Agent Environment execution.

* **Total Operations (Rows):** 1,070,917
* **Total Agent Task Tokens (Prompts only):** 231,577,252
* **Total Dataset Tokens (Full schema):** 243,218,984
* **Total Compute Expenditure (Generation):** 527,166,140 tokens (approx.)
* **Dimensionality:** 36 distinct professional archetypes spanning 17 macro-categories
* **Storage Format:** Chunked Parquet (`batch_id` ordered, Zstandard compression)
* **Tokenization Basal Metric:** OpenAI `cl100k_base`
* **Operational Length Distribution:** Gaussian cluster (μ = 175 words, σ = 15) strictly bounded by 80 (floor) and 400 (ceiling) thresholds.

### Core Operational Objective

This dataset abandons generic Q&A styling in favor of hyper-contextual "Agent Tasking." Each payload in this matrix is formulated as a first-person, highly technical diagnostic or execution command directed at an AI co-pilot embedded deep inside a specialized software application (DAW, NLE, 3D Suite, IDE, CAD, etc.).

The defining challenge lies in "Contextual Actuation"—the multimodal agent is routinely handed specific, highly technical tools or concepts but must systematically deduce the exact sequence of GUI actuations, node connections, or parameter adjustments required to resolve the contextual problem described. This dataset effectively fuses abstract text reasoning with executable software actuation.

## Parquet Schema & Encoding

The dataset schema is normalized for high-throughput data loading in multi-GPU training environments:

| Schema Node      | Data Type | Implementation Details                                                                                                             |
| :--------------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------------- |
| `batch_id`     | Int64     | Chronological generation marker (0 to 18,332). Acts as the primary deterministic seed for combinatorial permutation.               |
| `index_id`     | Int64     | Local index offset (0 to 49) representing the sub-batch chunk processed by the distributed asynchronous worker grid.               |
| `professional` | String    | The exact occupational archetype (e.g.,`Look Dev / Lighting TD`, `Audio Restoration Engineer`). Determines the lexical bounds. |
| `group`        | String    | The overarching macro-category (e.g.,`3D & CGI`, `Screen & Post Audio`) enabling stratified sampling.                          |
| `user_prompt`  | String    | The payload: The unformatted, raw task sequence requested of the multimodal agent.                                                 |

## Mathematics of Combinatorial Generation

To algorithmically ensure zero task duplication and eliminate monotonic semantic drift across 1.07 million rows, this dataset was generated via a multi-stage deterministic combinatorial engine:

**1. High-Fidelity Domain Taxonomies**<br>
The 36 archetypes are mapped against an expansive, highly specific software taxonomy. Generic terms (e.g., 'Compressor', 'Blur') were purged and replaced with high-fidelity, node-level and interface-level terminology (e.g., `program_dependent_compressor`, `subsurface_scattering_integrator`, `chroma_difference_keyer`). Each archetype possesses exactly 67 to 210 native tools.

**2. Pseudo-Random Intersection (The Tool Picker)**<br>
For each agent task, the engine executes a deterministic subset selection: selecting exactly $k \in \{2, 3\}$ tools from the available array $n$ for that specific professional.
With $n$ up to 210, the theoretical maximum unique combinatorial volume per professional is:

$$
{n \choose 2} + {n \choose 3} = C_{max}
$$

Summing this across the entire matrix produces **4,211,138** possible unique tool intersections. By sampling only 1,070,917 times from this pool using a seeded Random Number Generator bound to the `batch_id`, the dataset achieves high structural entropy while remaining computationally reproducible.

**3. Hash-Based Behavioral Injection**<br>
To shatter the monotonic voice often found in synthetic datasets, the task engine utilizes a 76-parameter behavioral array (featuring behaviors like `surgical`, `exasperated`, `clinical`, `deductive`). The behavior injected into the system prompt is chosen via:

$$
Style = Array[(batch\_id \times 1,000,003 + 17) \mod 76]
$$

This guarantees dynamic emotional and lexical variance per row while maintaining zero sequential correlation.

## The 36 Multimodal Environments

The dataset provides training scenarios across the complete spectrum of creative, technical, and engineering software interfaces.

### Agent Environment: Frontend & UI Infrastructure

* **Target Roles:** Frontend Designer (125,001 tasks), UI/UX Designer, Game UI Artist (27,027 tasks each)
* **Agent Operations:** In these domains, a fully competent AI agent must operate as a seamless translator between subjective design philosophy and rigorous, responsive structural code. The agent is expected to perceive the graphical canvas simultaneously as literal pixel data and as a living ecosystem of hierarchical dependencies, dynamic state logic, and accessibility constraints. A human operator expects the agent to autonomously traverse sprawling component architectures, anticipate how localized modifications will cascade across global styling frameworks, and maintain the aesthetic and functional integrity of an entire application across every conceivable device dimension and interactive scenario, executing the synthesis of form and function flawlessly.

### Agent Environment: 3D Visualization & Node-Based CGI

* **Target Roles:** 3D Animator, 3D Character Artist, CGI Generalist, Look Dev / Lighting TD, Product Visualization Artist, VFX Compositor, Motion Graphics Artist (27,027 tasks each)
* **Agent Operations:** Operating within infinite digital space, the agent is tasked with mastering the simulated physical laws that govern virtual universes. The AI must comprehend intricate spatial relationships, the computational mathematics of light behavior, the structural physics of materials, and the temporal flow of animation. Users demand that a competent agent can decipher massive, abstract procedural logic networks, proactively diagnose and resolve the cascading mathematical failures that corrupt rendering pipelines, and intuitively balance photorealistic fidelity against brutal computational efficiency. The agent must construct, animate, and light environments with the same comprehensive spatial intelligence as a master architect and cinematographer combined.

### Agent Environment: Nonlinear Editing (NLE) & Color Science

* **Target Roles:** Video Content Creator, Video Editor, Feature Film / TV Series Editor, Colorist / Color Grader (27,027 tasks each)
* **Agent Operations:** In these timeline-driven workspaces, reality is segmented into millions of sequential frames representing layered visual and auditory data streams. A multimodal agent must develop a profound temporal perception, intuitively grasping the psychological impact of pacing, editorial rhythm, and the profound emotional resonance of manipulated color gamuts. The human user expects the agent to autonomously conquer the chaos of vast, unstructured media ecosystems, dynamically sync decoupled data streams based on contextual observation, and execute complex, mathematically precise aesthetic transformations that seamlessly carry the emotional weight and narrative continuity of a cinematic vision from the first cut to the final master.

### Agent Environment: Digital Audio Workstations (DAW)

* **Target Roles:** Music Producer, Recording Engineer, Mixing Engineer, Mastering Engineer, Game Audio Designer, Sound Designer, Electronic Artist / DJ, Post-Production Audio Engineer, Broadcast Audio Engineer, Live Sound Engineer (In-the-Box), Audio Restoration Engineer, Classical Composer, Film & TV Composer, Singer-Songwriter, Vocalist / Performer (27,027 tasks each)
* **Agent Operations:** The DAW represents an entirely invisible ecosystem governed by psychoacoustics, frequency spectra, and shifting dynamic ranges, forcing the agent to translate dense, abstract visual telemetry into perfect sonic outcomes. The agent must intuitively understand the physical physics of overlapping soundwaves, the harmonic characteristics of engineered distortion, and the structural depth of three-dimensional mixing spaces. A competent agent is expected to parse the emotional intent behind a sprawling, multi-layered musical arrangement, effortlessly diagnosing structural sonic clashes, orchestrating vast routing architectures, and executing delicate, surgical interventions that elevate the artistic soul of the composition while adhering to unforgiving technical delivery standards.

### Agent Environment: Raster & Vector Design

* **Target Roles:** Brand Identity Designer, Packaging Designer, Digital Illustrator, Social Media Content Designer, Architectural Photographer, Fashion Retoucher, Photo Editor (27,027 tasks each)
* **Agent Operations:** Operating on the absolute frontier of visual aesthetics, the agent must master the inherent tension between the infinite mathematical precision of vector geometry and the destructive mutability of rasterized arrays. The operations demand an innate comprehension of compositional hierarchy, physiological perception of color volume, and the rigorous logic of non-destructive visual building blocks. The user expects the AI to look at a chaotic digital canvas and autonomously deduce the complex sequence of mathematical blend modes, geometric plottings, and subjective structural modifications required to conjure pixel-perfect art that resonates emotionally while maintaining pristine technical hygiene for final production.

## Application Context

The **Creative Professionals Agentic Tasks** dataset serves as core infrastructure for a diverse array of advanced AI architectures. Beyond powering standard visual action agents or localized software copilots, this dataset is built for the frontiers of autonomous execution—where agents act as full-fledged software delegates, application-spanning API orchestration drivers, and multi-modal problem solvers. It resolves the separation between conversational AI and functional, interface-aware autonomy.

A critical application of this dataset is infrastructure generation: developers can use a frontier AI model to instantly spin up a custom, isolated software environment tailored to a specific professional archetype (e.g., a simulated NLE timeline or node-based compositor). Because scaffolding this customized training infrastructure is now merely a five-hour feat, AI agents can be deployed into these bespoke environments to execute the tasks within this dataset, learning iteratively from their own interaction logs, terminal outputs, and structural feedback loops.

Because the data is grounded in the exact vernacular and pressure-tested scenarios of 36 distinct professions, models fine-tuned on this dataset gain profound contextual reasoning. They can interpret abstract, emotionally charged natural language workflows, decompose those workflows into a sequence of literal software actions, map those actions to underlying system APIs or UI paradigms, and execute them perfectly within professional-grade environments—without much human intervention or step-by-step hand-holding.

## Architect & Developer

This dataset, pipeline architecture, and underlying generation framework were engineered and mathematically bounded by Yatin Taneja.

As an AI System Engineer, Superintelligence Researcher, Dubstep artist, and poet, the motivation behind this dataset extends beyond pure system architecture. The goal is to push existing AI models to become fundamentally more creative and intuitive. By aggressively standardizing complex creative software into multi-dimensional arrays, this dataset forces AI agents to understand the essence of art and its human impact. These precise, structured agentic tasks are designed to create the next generation of AI agents, models that don't just execute commands, but possess the capacity to understand and facilitate the beauty that soothes the human experience.

### Weblinks

- **[IM Superintelligence](https://www.imsuperintelligence.ai):** Visit my central knowledge hub hosting other massive open datasets and over 2,000 articles exploring Superintelligence, cognitive architectures, quantum computing, distributed networks, algorithmic optimization, and the future of the global education sector, all authored through a custom 8-step multi-model agentic infrastructure I engineered.
- **[Yatin Taneja | Professional Portfolio](https://www.yatintaneja.in):** View my professional portfolio for a comprehensive overview of my skills, industry experience, and software prototypes as part of my ongoing engineering work in full-stack AI agents and applications.
- **[LinkedIn](https://www.linkedin.com/in/yatintaneja-pro/):** Connect on LinkedIn to collaborate on advanced autonomous systems, enterprise AI implementations, or to follow my ongoing research.

## License & Usage

This dataset is released under the **MIT License**.

Dedicated to advanced research in creative software orchestration, interface-aware autonomy, and complex multi-modal interaction across the creative industry stack. You are free to use this dataset for commercial, academic, and personal model training focused on executing high-fidelity technical tasks across 36 specialized professional environments, provided the original license and copyright notice are preserved.