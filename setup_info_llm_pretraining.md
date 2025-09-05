## LLM Pretraining Strategy

#### Pretraining datasets available on Huggingface
- [allenai/c4](https://huggingface.co/datasets/allenai/c4) (12.7TB with 305GB for en) : cleaned version of CommonCrawl
- [HuggingFaceFW/fineweb](https://huggingface.co/datasets/HuggingFaceFW/fineweb) (108TB) : cleaned and deduplicated english web data from CommonCrawl
- [HuggingFaceFW/fineweb-edu](https://huggingface.co/datasets/HuggingFaceFW/fineweb-edu) (10.4TB) : educational web pages filtered from FineWeb dataset
- [EleutherAI/pile](https://huggingface.co/datasets/EleutherAI/pile) (825GB) : 22 smaller, high-quality datasets combined together

#### Tokenization architecture recommended and used in major models
- [Byte-Pair Encoding](https://huggingface.co/learn/llm-course/en/chapter6/5)

#### Model architectures suitable for pretraininng from scratch
- [GPT-2](https://huggingface.co/docs/transformers/en/model_doc/gpt2)
- [GPT-Neo](https://huggingface.co/docs/transformers/en/model_doc/gpt_neo)
- [Llama 2](https://huggingface.co/docs/transformers/en/model_doc/llama2)
- [Mistral](https://huggingface.co/docs/transformers/en/model_doc/mistral)
- [Qwen3](https://huggingface.co/docs/transformers/en/model_doc/qwen3)

#### Pretraining framework
- Dataset preprocessing and streaming: [Huggingface Datasets](https://huggingface.co/docs/datasets/en/index)
- Model and tokenizer initialization: [Huggingface Transformers](https://huggingface.co/docs/transformers/en/index)
- Training framework: [Huggingface Trainer](https://huggingface.co/docs/transformers/en/main_classes/trainer)
- Multi-GPU setting: [Accelerate](https://huggingface.co/docs/accelerate/en/index) (torch.distributed)

#### Hardwares and OS for pretraining
- Recommended: 8 x NVIDIA H200 GPU (141GB)
- Acceptable: 8 x NVIDIA A100 GPU (80GB)
- OS: Ubuntu 24.04 LTS
