# Tuning Language Models by Proxy

## Challenge
- Large pretrained models become very resource intensive to fine-tune on specific domains.
- Difficult to rely on accessing LLMs parameters as some models are propietary (like GPT-3.5).

## Proxy Tuning 
- A decoding time algorithm designed to tune large pretrained LMs.
- Operates on top of black-box LMs by only accessing its predictions
- How? Uses smaller models and applies the difference in predictions between the proxy's tuned and untuned versions to guide the original larger model's prediction.

<img width="667" alt="Screenshot 2024-10-22 at 1 26 42 PM" src="https://github.com/user-attachments/assets/e04c5877-9a36-48c1-9842-d68c7485bd6f">

## Methodology
Give psuedocode


## Experiments

## Key Contributions

## Conclusions
- Efficient tuning for large models by modifying their output logits at runtime
- It improves accessibility of of LLMs because less computational resources are needed in order to fine-tune models.

## Critical Analysis
- There is a tradeoff between different metrics. Users must pick a balance between two desired attributes like truthfulness and informativeness.
- Large dependence on proxy model quality, it must be well-trained and fine-tuned to ensure high quality results
- Specific to language models where access to logits is possible, may not be as transferable to models like image generation. 





This repository contains code for the paper [Tuning Language Models by Proxy (2024)](https://arxiv.org/abs/2401.08565). If you have any questions, please feel free to create a Github issue or reach out to the first author at alisaliu@cs.washington.edu.

## Evaluation

You can download the evaluation data at [zip file of our evaluation data](https://github.com/alisawuffles/proxy-tuning/blob/main/data.zip). Our evaluation setup is largely borrowed from [Tülu 2](https://arxiv.org/abs/2311.10702) (codebase at https://github.com/allenai/open-instruct), with slight modifications. To see examples of how evaluation scripts are run, see `scripts/eval`.


## Citation
```
@misc{liu-etal-2024-tuning,
  title={Tuning Language Models by Proxy}, 
  author={Alisa Liu and Xiaochuang Han and Yizhong Wang and Yulia Tsvetkov and Yejin Choi and Noah A. Smith},
  year={2024},
  eprint={2401.08565},
  archivePrefix={arXiv},
  url={https://arxiv.org/abs/2401.08565}
}
```
