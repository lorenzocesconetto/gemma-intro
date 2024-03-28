# Gemma Intro

Authors: Lorenzo Cesconetto, Pedro Gengo.

## Running with llama.cpp

- Pre-requisite: You must have llama.cpp already installed and setup.

- Download from HF (please see [HF cli download reference](https://huggingface.co/docs/huggingface_hub/en/guides/download)):

```bash
pip install "huggingface_hub[hf_transfer]" # hf_transfer enables faster download
HF_HUB_ENABLE_HF_TRANSFER=1 huggingface-cli download google/gemma-2b-it gemma-2b-it.gguf # must set HF_HUB_ENABLE_HF_TRANSFER=1 for a faster download
```

- Quantized model:

```bash
./llama.cpp/quantize ../models_converted/gemma-2b-it.gguf ../models_quantized/gemma-2b-it-q8.gguf q8_0
```

- Running:

```bash
./llama.cpp/main 2>/dev/null \
    --model ./models_quantized/gemma-2b-it-q8.gguf \
    --ctx-size 8192 \
    --batch-size 8 \
    --keep -1 \
    --n-predict -1 \
    --color \
    --interactive-first \
    --temp 0.1 \
    --reverse-prompt "<start_of_turn>user " \
    --in-suffix "<start_of_turn>model " \
    --in-prefix "<end_of_turn> "
```
