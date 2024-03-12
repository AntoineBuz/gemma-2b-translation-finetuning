# gemma-2b-translation-finetuning

![App preview](img/banner.png)

This repository aims at giving minimal resources to finetune a 4-bits quantized (+ LoRA) version of Gemma-2B.
This is relevant in VRAM-limited environment as this is lightweight.

##  &#x2705; Prerequisites

- **Gemma access** : One needs a granted access to Gemma models. This can be done [accepting Google terms of use](https://huggingface.co/google/gemma-2b).
- **Gemma-2B-pretrained model** : Get a local [copy of the model](https://huggingface.co/google/gemma-2b) or import it with HuggingFace library.
- **Data** : The [opus-books (en-fr) dataset](https://huggingface.co/datasets/opus_books/tree/main/en-fr) can be found in the HuggingFace hub.
- **GPU** : I made the model fit (during training - see batch_size below) in a RTX3080 (10GB VRAM)
- **Required packages** : Required packages can be installed with the given `requirements.txt`

## Dataset : `opus_books`

For this project we will be using an en-fr corpus taken from the HuggingFace hub.It is made of roughly 130k couples of en-fr translations.

|     | **English**                                                                                            | **French**                                                                                           |
|-----|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| 1   | He arrived at our home on a Sunday of November, 189-.                                              | Il arriva chez nous un dimanche de novembre 189-…                                                |
| 2   | I still say 'our home,' although the house no longer belongs to us.                                | Je continue à dire « chez nous », bien que la maison ne nous appartienne plus.                   |
| 3   | We left that part of the country nearly fifteen years ago and shall certainly never go back to it. | Nous avons quitté le pays depuis bientôt quinze ans et nous n’y reviendrons certainement jamais. |
| ... |                                                 ...                                                |                                                ...                                               |

## &#127899; Fine-tuning process

![Process](img/diagram.png)


## &#128201; Some results

After a training of roughly 5 hours I have already been able to notice interesting results.

- **Here is the loss curve I have got**

![Loss along steps](img/loss.png)

- &#127881; **Despite "too-long" outputs, let's have a look on several translations :**

|                                             | **pretrained**       | **finetuned**                            |
|---------------------------------------------|---------------------|------------------------------------------------|
| **Thank you.**                                  | *repeated question without translating* | Merci.                                         |
| **Training it was very interesting !**         | *repeated question without translating* | L'entraînement était très intéressant !        |
|**I am not that good at translating to French** | *repeated question without translating* | Je ne suis pas très bon à traduire en français |

*See `finetuning.ipynb` for detailed config (temperature, max_lenght...)*

## &#128218; References

Gemma-2B pretrained is taken from [Google on HuggingFace](https://huggingface.co/google/gemma-2b)

The en-fr dataset is taken from [en-fr Opus_books on HuggingFace](https://huggingface.co/datasets/opus_books/tree/main/en-fr)

The given `finetuning.ipynb` is inspired by [this repository](https://github.com/adithya-s-k/LLM-Alchemy-Chamber/blob/main/Finetuning/Gemma_finetuning_notebook.ipynb)
