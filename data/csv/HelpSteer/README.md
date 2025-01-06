---
license: cc-by-4.0
language:
- en
pretty_name: Helpfulness SteerLM Dataset
size_categories:
- 10K<n<100K
tags:
  - human-feedback
dataset_info:
  features:
    - name: prompt
      dtype: string
    - name: response
      dtype: string
    - name: helpfulness
      dtype: int32
    - name: correctness
      dtype: int32
    - name: coherence
      dtype: int32
    - name: complexity
      dtype: int32
    - name: verbosity
      dtype: int32
  splits:
    - name: train                  
      num_examples: 35331
    - name: validation                  
      num_examples: 1789
---

# HelpSteer: Helpfulness SteerLM Dataset


HelpSteer is an open-source Helpfulness Dataset (CC-BY-4.0) that supports aligning models to become more helpful, factually correct and coherent, while being adjustable in terms of the complexity and verbosity of its responses.

Leveraging this dataset and SteerLM, we train a Llama 2 70B to reach **7.54** on MT Bench, the highest among models trained on open-source datasets based on [MT Bench Leaderboard](https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard) as of 15 Nov 2023.
This model is available on HF at [Llama2-70B-SteerLM-Chat](https://huggingface.co/nvidia/Llama2-70B-SteerLM-Chat).

Try this model instantly for free hosted by us at [NVIDIA AI Playground](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/ai-foundation/models/llama2-70b-steerlm). You can use this in the provided UI or through a limited access API (up to 10, 000 requests within 30 days). 
If you would need more requests, we demonstrate how you can set up an inference server at [Llama2-70B-SteerLM-Chat model page on HF](https://huggingface.co/nvidia/Llama2-70B-SteerLM-Chat)

You can also train a model using [NeMo Aligner](https://github.com/NVIDIA/NeMo-Aligner) following [SteerLM training user guide](https://docs.nvidia.com/nemo-framework/user-guide/latest/modelalignment/steerlm.html).

<img src="https://huggingface.co/datasets/nvidia/HelpSteer/resolve/main/mtbench_categories.png" alt="MT Bench Categories" width="800" style="margin-left:'auto' margin-right:'auto' display:'block'"/>


HelpSteer Paper : [HelpSteer: Multi-attribute Helpfulness Dataset for SteerLM](http://arxiv.org/abs/2311.09528)

SteerLM Paper: [SteerLM: Attribute Conditioned SFT as an (User-Steerable) Alternative to RLHF](https://arxiv.org/abs/2310.05344)

Note: [HelpSteer2](https://huggingface.co/datasets/nvidia/HelpSteer2) is the follow up to this dataset and we recommend using HelpSteer2 instead of this dataset.


## Dataset Description

HelpSteer contains 37, 120 samples, each containing a prompt, a response as well as five human-annotated attributes of the response, each ranging between 0 and 4 where higher means better for each attribute.

These attributes are:

1. **Helpfulness**: Overall helpfulness of the response to the prompt.
2. **Correctness**: Inclusion of all pertinent facts without errors. 
3. **Coherence**: Consistency and clarity of expression. 
4. **Complexity**: Intellectual depth required to write response (i.e. whether the response can be written by anyone with basic language competency or requires deep domain expertise).
5. **Verbosity**: Amount of detail included in the response, relative to what is asked for in the prompt.


## Example

```json
{
  "prompt": "What are the three most important things to consider when deciding what technology to use to build an assist device to help an elderly person with basic needs?",
  "response": "To build an assistive device to help an elderly person with basic needs, one must consider three crucial things: safety, compatibility, and ease of use. Safety is paramount, as the device must not cause harm to the user. Compatibility with the user's environment and other devices is also essential. Finally, the device must be simple enough for the elderly person to operate.",
  "helpfulness": 3,
  "correctness": 4,
  "coherence": 4,
  "complexity": 2,
  "verbosity": 2
}
```


## Using the Huggingface Datasets

```python
from datasets import load_dataset

ds = load_dataset("nvidia/HelpSteer")

train = ds['train'] # len(train) = 35331 (95%)
val = ds['validation']     # len(val) = 1789 (5%)
```

## Source

1. Prompts are collected based on a mixture of template-generated (mainly for prompt involving long reference text) and human generated by Scale AI. These prompts relate to the tasks of Rewrite, Summarization, Classification, Extraction, Closed Question Answering, Open Question Answering, Generation and Brainstorming.
2. Responses are generated by an early version of an inhouse LLM. We generate up to 4 responses per prompts using sample techniques to give diverse yet reasonable responses.
3. Annotations of various attributes were done by Scale AI. Annotators rated each response on a Likert 5 scale (between 0 and 4) for each attribute (helpfulness, correctness, coherence, complexity and verbosity).

## Annotation methodology (short)	

1. We engaged a select group of contractors via Scale AI. These contractors were provided with comprehensive guidelines that defined each attribute and the criteria for every rating level, together with some annotated examples. These guidelines and examples are detailed in the Appendix of the accompanying paper.
2. The annotation process involved approximately 200 U.S.-based human annotators. Candidates first underwent preliminary assignments, including assessments of English proficiency, to determine eligibility for working on the project. Subsequently, they participated in an introductory training course on the task which ended with a test that involved annotating 35 sample responses. This process ensured not only a thorough understanding of the task requirements but also the delivery of high-quality annotations.
3. Post-annotations, Scale AI performed extensive quality assurance, with each annotation reaching a minimum of two human reviews in addition to automated checks. After receiving the annotations from Scale AI, we conducted our independent quality assurance to make sure that the quality of the annotations was up to our expectations. As a result, some annotations were filtered away to retain only 37, 120 samples. 


## Ethical statement	
Annotators for the dataset were contracted through Scale AI. Scale AI engages the Anker Methodology, GISC Impact Sourcing Standard, and UN Sustainable Development Goals to provide a fair and competitive pay. The specific pay is calculated based on many factors, including the specific project, the specialized skillset and expertise required, regional costs of living and then transparently listed on Scale AI platform. Scale AI also provides multiple channels for questions and support, including 24/7 support teams, community discussion channels with specially trained moderators, and a “speak up” hotline where contractors can report concerns anonymously. Worker concerns can be submitted to and are reviewed by our Remotasks support team, and pay disputes are reviewed by support specialists trained in this area. 


## Citation

If you find this dataset useful, please cite the following works

```bibtex
@misc{wang2023helpsteer,
      title={HelpSteer: Multi-attribute Helpfulness Dataset for SteerLM}, 
      author={Zhilin Wang and Yi Dong and Jiaqi Zeng and Virginia Adams and Makesh Narsimhan Sreedhar and Daniel Egert and Olivier Delalleau and Jane Polak Scowcroft and Neel Kant and Aidan Swope and Oleksii Kuchaiev},
      year={2023},
      eprint={2311.09528},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

```bibtex
@misc{dong2023steerlm,
      title={SteerLM: Attribute Conditioned SFT as an (User-Steerable) Alternative to RLHF}, 
      author={Yi Dong and Zhilin Wang and Makesh Narsimhan Sreedhar and Xianchao Wu and Oleksii Kuchaiev},
      year={2023},
      eprint={2310.05344},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```
