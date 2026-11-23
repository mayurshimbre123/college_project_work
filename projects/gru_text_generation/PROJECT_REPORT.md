# Synthetic text generation — character-level GRU

## What I was exploring

Could a recurrent neural network produce text one character at a time? The notebook walks through reading Shakespeare lines, lowercasing, mapping Unicode characters to integer IDs, batching, a two-layer GRU language model in Trax, and sampling.

## Mechanics

- Input line becomes a sequence of character IDs. Example: `'abc xyz' → [97,98,99,32,120,121,122,1]` (1 marks end of sequence).
- Network: `ShiftRight → Embedding(256,512) → GRU(512) → GRU(512) → Dense(256) → LogSoftmax`.
- Original outputs show **125,097 lines**, with **124,097** training lines and **1,000** holdout lines.
- The displayed training demo runs **one optimization step**; it is not enough to explain the reported checkpoint performance.

## Reported result and provenance

Another cell loads `model.pkl.gz` using `model.init_from_file(...)` and prints log perplexity **1.9785146** and perplexity **7.2319922**. It is a **saved-checkpoint evaluation**, not a score achieved by the one-step training demonstration. Without that checkpoint and original data files, I cannot reproduce this number or claim who/what trained the checkpoint.

## Follow-up

Recover `data/` and `model.pkl.gz` from the original environment if permitted; identify checkpoint origin, run evaluation on unseen data, and compare sampling temperatures. The model is historical coursework, not a modern LLM training benchmark.

See `original/Synthetic_Text_Generation.ipynb` for original source and outputs.

The recurrent update and reset gates control how much prior hidden state is carried forward or used to form a candidate state. Perplexity is exp(mean token negative log likelihood); the review notebook reproduces the exponentiation, independent of the missing checkpoint.
