# Deep Learning Coursework — University of Mississippi

Selected project submissions from a graduate-level Deep Learning course. Each project was implemented from scratch in Python using PyTorch and the D2L framework, with written analysis of results.

---

## Project 2: Recurrent Neural Networks

**Part 1 — RNN from scratch**

Implemented a character-level RNN language model from scratch, including the forward pass, hidden state updates, and backpropagation through time. Conducted a systematic hyperparameter study varying the number of hidden units, sequence length (num\_steps), learning rate, and training epochs. Evaluated models by tracking training and validation perplexity, with particular attention to the train-validation gap as a signal for overfitting. Also tested the effect of gradient clipping on training stability.

**Part 2 — GRU from scratch**

Implemented a Gated Recurrent Unit (GRU) from scratch, including the reset and update gate computations. Compared behavior against the baseline RNN from Part 1.

---

## Project 3: Attention Mechanisms

**Part 1 — Bahdanau (additive) attention**

Built a sequence-to-sequence model for English-to-French translation using a GRU encoder and a GRU decoder with Bahdanau attention. Unlike a fixed context vector, the attention mechanism lets the decoder focus on different encoder positions at each decoding step. Evaluated models using BLEU score and visualized learned attention weights as heatmaps to interpret alignment between source and target tokens.

**Part 2 — Multi-head attention**

Extended the Seq2Seq model from Part 1 by replacing the single attention head with multi-head attention. Evaluated translation quality on a held-out test set and visualized the attention distribution for each head separately. Analysis showed that while different heads occasionally attended to distinct source positions, several heads were largely redundant on this dataset.

---

## Project 5: AI Agent Pipeline for LaTeX Project Compression

Designed and implemented a multi-step agentic pipeline in Python to reduce the size of a large LaTeX project (originally 118 MB) while preserving the visual quality of the compiled PDF.

The pipeline followed an analysis → decision → action → verification structure:

- **Analysis agent** — scanned `.tex` files to identify which figures were actively referenced via `\includegraphics`, separating used assets from backups and duplicates.
- **Decision agent** — classified files as removable (backups, unused figures, nested duplicates) versus necessary, moving rather than deleting to allow safe rollback.
- **Action agent** — removed the backups folder, relocated unused figures, and applied moderate JPEG compression via macOS `sips` to remaining images.
- **Verification agent** — compiled the optimized project and checked that all figures were present and visually acceptable in the final PDF.

**Results:** The optimized source zip was reduced from 118 MB to 16 MB; the compiled PDF was 17 MB, meeting both the 50 MB source and 30 MB PDF requirements. The pipeline deliberately reserved foundation model API calls for judgment-intensive tasks (e.g., visual quality assessment) rather than file analysis, which was handled entirely by deterministic Python code.

Full report: [project5/index.md](project5/index.md)
