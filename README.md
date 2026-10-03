<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/ANTI-Tony/ANTI-Tony/main/assets/masthead-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/ANTI-Tony/ANTI-Tony/main/assets/masthead-light.svg">
    <img src="https://raw.githubusercontent.com/ANTI-Tony/ANTI-Tony/main/assets/masthead-light.svg" width="560" alt="Jingbo Wen (Tony) — LLM systems, efficient inference, compute allocation">
  </picture>
  <br><br>
  <a href="https://jtw-sable.vercel.app">Homepage</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://scholar.google.com/citations?user=iWXqUoEAAAAJ">Google&nbsp;Scholar</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="mailto:jingbowen46@gmail.com">Email</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://www.linkedin.com/in/tony-wen-170461283/">LinkedIn</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://juejin.cn/user/4100551259985721">Juejin</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://jtw-sable.vercel.app/zh">中文</a>
</div>

<br>

I build and study infrastructure for large language models: inference serving, speculative decoding, and distributed training. I am completing a B.Eng. (Hons) in Software Engineering at the University of Sydney. Most recently I was an Applied Scientist Intern at Microsoft, working on foundation-model serving; before that, an Agent Engineering Intern at Xiaohongshu (RedNote). My research is on allocating inference compute: consequence-aware reasoning budgets and visual token compression, budget-robust speculative decoding, reward-aware execution gating for agents, and market-aware routing across inference providers.

*Open to LLM Engineer / LLM Infrastructure roles.*

## Research

1. [Not All Errors Are Equal: Consequence-Aware Reasoning Compute Allocation](https://arxiv.org/abs/2606.04402)<br>
   Liang He, **Jingbo Wen**, Haoyu Wang, Ziqi He, Yixiong Chen, Kangning Cui, Xilu Wang<br>
   *arXiv:2606.04402, 2026.* 22–33% lower cost-weighted loss than difficulty-aware compute routing on SWE-bench Lite.

2. [BudgetDraft: Acceptance-Aware Multi-View Training for Sparse-KV Speculative Decoding](https://arxiv.org/abs/2606.00144)<br>
   Liang He, **Jingbo Wen**, Qishi Zhan, Yixiong Chen, Kangning Cui, Qizhen Lan, Xilu Wang<br>
   *arXiv:2606.00144, 2026.* One budget-robust drafter for sparse KV Cache; 6.55× end-to-end speedup at 4K context. [[code]](https://github.com/ANTI-Tony/BudgetDraft)

3. [Not All Visual Tokens Are Equally Safe to Remove: Consequence-Sensitive Visual Token Compression](https://arxiv.org/abs/2608.09176)<br>
   **Jingbo Wen**, Liang He, Mingyu Cao, Haoyu Wang, Minxuan Hu, Kangning Cui, Xilu Wang<br>
   *arXiv:2608.09176, 2026.* High-stakes VLM errors 0.300 → 0.133 at fixed token budget; 38% lower cost-weighted error.

4. [From Relevance to Execution Utility: Reward-Aware Dynamic Execution Gating for Skill-Based LLM Agents](https://arxiv.org/abs/2608.09168)<br>
   Liang He, **Jingbo Wen**, Hongyu Gu, Hao Li, Haoyu Wang, Yixiong Chen, Kangning Cui, Xilu Wang<br>
   *arXiv:2608.09168, 2026.* RADEG skips 68% of agent calls while retaining 61% of total reward.

5. [You Cannot Pick a Provider From the Price List: Market-Aware Routing for Open-Weight LLM Inference](https://arxiv.org/abs/2609.37902)<br>
   Liang He, **Jingbo Wen**, Yixiong Chen, Yue Yang, Qizhen Lan, Kangning Cui, Xilu Wang<br>
   *arXiv:2609.37902, 2026.* Price does not predict quality; measured routing saves ~50% at matched quality.

## Experience

**Microsoft** — Applied Scientist Intern, Azure community infra<br>
<sub>Jun 2026 – Sep 2026</sub>

- Built a dynamic-batching request scheduler in **Go** for Foundation Model serving (routing, admission control, deadlines), sustaining 2K+ concurrent streams; cut p99 TTFT by **28%** under bursty traffic.
- Integrated **EAGLE-3 speculative decoding** into the serving runtime, with per-request KV-cache rollback so batches with unequal acceptance lengths verify in one pass; **1.8×** tokens/s at mean acceptance length 3.6.
- Profiled the scheduler-to-GPU path with pprof and Nsight Systems; traced a TPOT regression to per-token scheduler–runtime RPC overhead and removed it with batched streaming, lowering TPOT by **17%**.
- Built benchmarking and observability for **TTFT, TPOT, tokens/s, and KV-cache usage** across batch sizes and speculation configs; its load sweeps set the concurrency threshold above which speculation is disabled.

**Xiaohongshu (RedNote)** — Agent Engineering Intern, Social Networking Engineering<br>
<sub>Dec 2025 – Mar 2026</sub>

- Designed and developed an internal **Coding Agent** from 0→1, enabling autonomous codebase understanding, multi-file editing, tool use, code execution, and iterative debugging from natural-language instructions.
- Built a **0→1 OCR verification pipeline** (extraction, validation, exception handling) for a production mobile app and took it from prototype to launch: **98% verification accuracy**, **21K+ users verified on day one**.
- Optimized LLM serving (**vLLM, INT4 quantization, continuous batching**): **+45% QPS**, **−40% cost**.
- Built and maintained internal LLM training and evaluation pipelines supporting **SFT / DPO / RLHF** workflows.

## Projects

**Distributed LLM Training & Inference System** — personal project, LLM Systems / Distributed Computing<br>
<sub>Jan 2026 – Present</sub>

- Implemented a 350M–1.3B GPT-style Transformer from scratch (**GQA, RoPE, SwiGLU, RMSNorm**).
- Built **Megatron-style Tensor Parallelism** (Column/RowParallelLinear, VocabParallelEmbedding) and **Pipeline Parallelism** (GPipe / 1F1B scheduling, P2P activation transfer, pipeline bubble analysis).
- Integrated **DeepSpeed ZeRO-1/2/3** with CPU Offload into a **3D parallel training stack (TP × PP × DP)**, pre-training a 1.3B model on **4×A100** (TP=2, PP=2) over 1.5B tokens.
- Built a **KV Cache inference engine** (Prefill/Decode separation, dynamic batching, O(n) per-step attention).
- Wrote custom **CUDA C++ and Triton kernels** (elementwise fusion, reduction, softmax/LayerNorm, tiled matmul) and profiled them against PyTorch native ops with Nsight Compute.

## Skills

<table>
  <tr><td><b>LLM&nbsp;Training</b></td><td>LoRA · SFT / DPO / RLHF · DDP · Tensor / Pipeline Parallelism · DeepSpeed ZeRO-1/2/3 · NCCL</td></tr>
  <tr><td><b>LLM&nbsp;Inference</b></td><td>KV Cache · Paged Attention · Speculative Decoding · Quantization · vLLM · TensorRT-LLM</td></tr>
  <tr><td><b>GPU&nbsp;&amp;&nbsp;Kernel</b></td><td>CUDA C++ · Triton · Nsight Compute · CUDA Streams / Events</td></tr>
  <tr><td><b>ML&nbsp;Engineering</b></td><td>PyTorch · Go · FAISS · ChromaDB · RAG · FastAPI · Docker · Linux · Git</td></tr>
</table>

## Education

**University of Sydney** — B.Eng. (Hons), Software Engineering (ECE)<br>
<sub>Mar 2023 – Mar 2027 (expected)</sub>

GPA 3.8 / 4.0 · 2025 Dean’s List · TOEFL iBT 110 / 120 (5.5 / 6)

## Writing

I write 拆解大模型 (“Taking LLMs Apart”), a series in Chinese on [Juejin](https://juejin.cn/user/4100551259985721) about how large language models work: language modeling, Transformer internals, attention, and training.

<br>

<div align="center">
  <sub>More at <a href="https://jtw-sable.vercel.app">jtw-sable.vercel.app</a> · Last updated October 2026</sub>
</div>
