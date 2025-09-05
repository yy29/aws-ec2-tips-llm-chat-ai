## LLM Pretraining

#### Pretraining datasets available on Huggingface
- [allenai/c4](https://huggingface.co/datasets/allenai/c4) (12.7TB with 305GB for en)
- [HuggingFaceFW/fineweb](https://huggingface.co/datasets/HuggingFaceFW/fineweb) (108TB)
- [HuggingFaceFW/fineweb-edu](https://huggingface.co/datasets/HuggingFaceFW/fineweb-edu) (10.4TB)
- [EleutherAI/pile](https://huggingface.co/datasets/EleutherAI/pile) (825GB)

#### Tokenization architecture recommended
- [Byte-Pair Encoding](https://huggingface.co/learn/llm-course/en/chapter6/5)

#### Model architectures suitable for pretraininng from scratch
- [GPT-2](https://huggingface.co/docs/transformers/en/model_doc/gpt2)
- [GPT-Neo](https://huggingface.co/docs/transformers/en/model_doc/gpt_neo)
- [Llama 2](https://huggingface.co/docs/transformers/en/model_doc/llama2)
- [Mistral](https://huggingface.co/docs/transformers/en/model_doc/mistral)

#### Pretraining framework
- Dataset preprocessing and streaming: [Huggingface Datasets](https://huggingface.co/docs/datasets/en/index)
- Training framework: [Huggingface Trainer](https://huggingface.co/docs/transformers/en/main_classes/trainer)
- Multi-GPU setting: [Accelerate](https://huggingface.co/docs/accelerate/en/index)
