# Fine-tuning GPT-3
This document explains the complete process of fine-tuning of GPT-3  
models. It also explains how to generate the dataset in required format  
for tine-tuning GPT-3 models, and also how to analyze the fine-tuned  
model and its various metrics.  
<br>
GPT-3 has been pre-trained on a vast amount of text from the open  
internet. When given a prompt with just a few examples, it can often  
intuit what task you are trying to perform and generate a plausible  
completion. This is often called "few-shot learning."  
<br>
Fine-tuning improves on few-shot learning by training on many more   
examples that can fit in the prompt, letting you achieve better results  
on a wide number of tasks. Once a model has been fine-tuned, you won't  
need to provide examples in the prompt anymore.  
<br>  
At a high level, fine-tuning involes the following steps:  
1. Prepare and upload training data
2. Train a new fine-tuned model
3. Use your fine-tuned model


## What models can be fine-tuned?
Fine-tuning is currently only available for the following base-models:  
- `davinci`, which is the most capable GPT-3 model. It can do any task  
the other models can do, often with higher quality. Max tokens is   
limited to 2,049 and training data is upto Oct, 2019.  
<br>
- `curie`, which is very capable, but faster and lower cost than `davinci`.  
Max tokens is limited to 2,049 and training data is upto Oct, 2019.  
<br> 
- `babbage`, which is capable of straightforward tasks, very fast, and  
lower cost. Max tokens is limited to 2,049 and training data is upto  
Oct, 2019.  
<br>
- `ada`, which is capable of very simple tasks, usually the fastest model  
in the GPT-3 series, and lower cost. Max tokens is limited to 2,049 and  
training data is upto Oct, 2019. 

These are the original models that do not have any instruction following  
training (like text-davinci-003 does for example). You can also  
[continue fine-tuning a fine-tuned model](https://platform.openai.com/docs/guides/fine-tuning/continue-fine-tuning-from-a-fine-tuned-model) to add additional data without  
having to start from scratch.


## Fine-tune GPT-3
### Installation:
Install the OpenAI python library by running:
> pip install --upgrade openai

Set your `OPENAI_API_KEY` environment variable by adding the following  
line into your shell initialization script or running it int eh command  
line before the fine-tuning command:
> export OPENAI_API_KEY="<OPENAI_API_KEY>"

### Prepare training data:
[This](TRAINING%20DATA.md) document explains all the steps needed to prepare your training  
data for fine-tuning GPT-3 along with the best practices and specific  
guidelines.

### Create a fine-tuned model
[This](CREATE%20FINE-TUNED%20MODEL.md) document explains all the steps needed to create  
your fine-tuned model and start the training.   

### Use a fine-tuned model
[This](USE%20FINE-TUNED%20MODEL.md) document explains how to use the fine-tuned model  
for inference.
