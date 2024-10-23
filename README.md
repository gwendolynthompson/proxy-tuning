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
1. M: pretrained large model 
2. M-: pretrained, smaller untuned model (with the same vocabulary as M)
3. M+: M- after tuning, directly fine tuned on the target task or domain
<img width="552" alt="Screenshot 2024-10-22 at 2 08 27 PM" src="https://github.com/user-attachments/assets/4924c7a0-f66c-47c4-8646-564c39868bc7">

- Adds the difference of the logit of M+ and M- to the logit of M which allows only newly learned information to go into M as opposed to general model knowledge.
- Takes the softmax to convert to logit into a probability distribution which is the output.

### Balancing truthfulness and informativeness
<img width="656" alt="Screenshot 2024-10-23 at 11 49 59 AM" src="https://github.com/user-attachments/assets/c44a6c24-71d0-4e26-bd7d-9ec65b6d7e53">

<img width="285" alt="Screenshot 2024-10-22 at 2 19 19 PM" src="https://github.com/user-attachments/assets/37a0e273-0d7a-4d1a-9d5d-e30d4f907b03">

**Truthfulness:** Whether or not the content is factually accurate. No misleading or false statements.
**Informativeness:** Refers to the level of detail/richness of the content. More context/background but may not all be needed to answer the question.



## Experiments & Results
### Instruction Tuning 
- Alpacafarm (open-ended instructions) and GSM (arithmetic word problems): closed 88% of the gap between base and fully versions 
- ToxiGen (evaluates toxicity of model generations): untuned produced toxic content 67-70% of the time, proxy tuning brought it to 0%
- TruthfulQA (evaluates knowledge and reasoning): proxy model was 3.2 to 6.5% more truthful.

### Task specific tuning 
- TriviaQA (question answering):
  - 13B there was 19.1% improvement
  - 70B there was a 17.5% improvement
- GSM (math word problems):
  - 13B there was a 37.3% improvement
  - 70B there was a 44.3% improvement

### Code adpatation
- codexEval (generating python functions):
  - 13B, 32% improvement
  - 70B there was a 8.6% improvement
- DS-100 (python programming problems):
  - 13B there was a 16.6% improvement
  - 70B there was a 6.7% improvement



## Impacts
- Addresses one of the major challenges in LLMs: **efficent fine-tuning** which enables people to adapt large, pretrained models to new tasks without as many resources.
- Builds on research in **transfer learning and fine-tuning**. It extends the previous ideas without needing access to the model's parameters.
- Provides new methods for handling **proprietary models**.

## Critical Analysis
- There is a tradeoff between different metrics. Users must pick a balance between two desired attributes like truthfulness and informativeness.

- Large dependence on proxy model quality, it must be well-trained and fine-tuned to ensure high quality results

- Specific to language models where access to logits is possible, may not be as transferable to models like image generation.


## Conclusions
- Efficient tuning for large models by modifying their output logits at runtime
- It improves accessibility of of LLMs because less computational resources are needed in order to fine-tune models.


## Resource Links 
- "The Power of Proxy Data and Proxy Networks for Hyper-Parameter Optimization" https://arxiv.org/abs/2107.05471
- "Improve LLMs With Proxy Tuning" https://lightning.ai/lightning-ai/studios/improve-llms-with-proxy-tuning
- "LoFT: Local Proxy Fine-tuning Improves Transferability to Large Language Model Attacks" https://openreview.net/forum?id=3ucOvX8WVu
- "CPT: COnsistent Proxy Tuning for Black-box Optimization" https://www.researchgate.net/publication/381885086_CPT_Consistent_Proxy_Tuning_for_Black-box_Optimization 







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
