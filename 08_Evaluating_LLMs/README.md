# Evaluating LLMs and Potential Pitfalls

Intro to AI-Driven Science on Supercomputers @ ALCF 2024

**Contact:** Marieme Ngom ([mngom@anl.gov](mailto:///mngom@anl.gov)), Bethany Lusch ([blusch@anl.gov](mailto:///blusch@anl.gov)), Sandeep Madireddy  ([smadireddy@anl.gov](mailto:///smadireddy@anl.gov)) 


[Overview of LLMs Evaluation](https://github.com/argonne-lcf/ai-science-training-series/blob/main/08_Evaluating_LLMs/LLM_Evaluation_Overview.pdf)

[Potential Pitfalls of LLMs](https://github.com/argonne-lcf/ai-science-training-series/blob/main/08_Evaluating_LLMs/LLM-Pitfalls.pdf)
    
[Link to breakout rooms forms](https://drive.google.com/drive/folders/1BN_aBlNU-7KVIcySntRtbkBXRGpkMSyz)

Other helpful links:
- [OpenAI tokenizer](https://platform.openai.com/tokenizer)
- [Chatbot Arena](https://chat.lmsys.org/)
- [Chatbot Guardrails Arena](https://huggingface.co/spaces/lighthouzai/guardrails-arena)

 
 **Homework**
 
What do you think is a particularly good use case for LLMs for science? How would you evaluate it?
Your answer does not need to be in paragraphs. When you submit your homework form, you can link to a file in your Github repo where you wrote your answer.


**Answer**

I feel that LLMs can be used in various aspects of DNA sequence modeling. In terms of evaluation, I think establishing **performance benchmarking** with DNA sequence modeling is a much more complicated task than language modeling. To begin with, the "connection" between the thing we **want** to predict (biological effects of DNA sequence) and the data we are using to train the model is more indirect. For example, DNA models which are trained to "generatively" predict DNA sequence similar to chatbots can produce plenty of "novel" outputs. Evaluating these, however, requires the generated sequences to be experimentally evaluated in living biological systems to assess whether they are viable biological signal. This is very laborious and costly relative to standard language systems which can receive quick feedback from regular users. It also highlights an issue with **alignment with desired outcomes**, because it is a contradiction to be able to train a model to predict novel discoveries using already-discovered corpus' of data. 

Existing DNA sequence models already wrestle extensively with **ethical considerations**. These considerations must also apply to LLM-based DNA sequence models. For example, DNA-sequence predictors of personalized phenotypes (polygenic risk models), are prone to bias in composition of the training data. Genetic variation is noisy, and is always confounded by external environmental factors which correlate with both phenotype and inter-individual DNA sequence variation. Poorly trained LLMs will inevitably make similar mistakes and must be evaluated for such biases.
