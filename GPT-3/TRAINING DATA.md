# Prepare Training Data for Fine-tuning GPT-3

Training data is how you teach GPT-3 what you'd like it to say.  
<br> 
Your data must be a [JSONL](JSON%20LINES.md) document, where each line  
is a prompt-completion pair corresponding to a training example. A  
sample document is given below:
> {"prompt": "&lt;prompt text&gt;", "completion": "&lt;ideal generated text&gt;"}  
> {"prompt": "&lt;prompt text&gt;", "completion": "&lt;ideal generated text&gt;"}  
> {"prompt": "&lt;prompt text&gt;", "completion": "&lt;ideal generated text&gt;"}  
> ...  

Designing your prompts and completions for fine-tuning is different  
from designing your prompts for use with base models. In particular,  
while prompts for base models often consist of multiple examples, for  
fine-tuning, each training example generally consists of a single input  
example and its associated output, without the need to give detailed  
instructions or include multiple examples in the same prompt. 
<br>  
The more training examples you have, the better. In general, each  
doubling of the dataset size leads to a linear increase in model quality.  

## CLI Data Preparation Tool
OpenAI developed a tool which validates, gives suggestions, and reformats  
your data:
> openai tools fine_tunes.prepare_data -f <LOCAL_FILE>

This tools accepts different formats, with the only requirement that  
they contain a prompt and a completion column/key. You can pass a **CSV,  
TSV, XLSX, JSON, or JSONL** file, and it will save the output into a JSONL  
file ready for fine-tuning, after guiding you through the process of  
suggested changes. 


## Best Practices for Preparing Dataset
### Data Formatting
To fine-tune a model, you'll need a set of training examples that each  
consist of a single input ("prompt") and its associated output  
("completion"). This is notably different from using the base models,   
where you might input detailed instructions or multiple examples in a   
single prompt.

- Each prompt should end with a fixed separator to inform the model when  
the prompt ends and the completion begins. A simple separator which  
generally works well is `\n\n###\n\n`. The separator should not appear  
elsewhere in any prompt.  
<br>  
- Each completion should start with a whitespace due to the tokenization,  
which tokenizes most words with a preceding whitespace.  
<br>
- Each completion should end with a fixed stop sequence to inform the  
model when the completion ends. A stop sequence could be `\n`, `###`, or  
any other token that does not appear in any completion.  
<br>
- For inference, you should format your prompts in the same way as you  
did when creating the training dataset, including the same separator.  
Also specify the same stop sequence to properly truncate the completion.  


### General Best Practices
Fine-tuning performs better with more high-quality examples. To   
fine-tune a model that performs better than using a high-quality prompt  
with the base models, you should provide at least a few hundred   
high-quality examples, ideally vetted by human experts. From there,  
performance tends to linearly increase with every doubling of the number  
of examples. Increasing the number of examples is usually the best and  
most reliable way of improving performance.  

Classifiers are the easiest models to get started with. For classification  
problems we suggest using `ada`, which generally tends to perform only  
very slightly worse than more capable models once fine-tuned, whilst  
being significantly faster and cheaper.  

If you are fine-tuning on a pre-existing dataset rather than writing  
prompts from scratch, be sure to manually review your data for offensive  
or inaccurate content if possible, or review as many random samples of  
the dataset as possible if it is large.  


### Specific Guidelines for Conditional Generation
Conditional generation is a problem where the content needs to be  
generated given some kind of input. This includes paraphrasing,  
summarizing, entity extraction, product description writing given  
specifications, chatbots and many others. For this type of problem we  
recommend:

- Use a separator at the end of the prompt, e.g. `\n\n###\n\n`. Remember  
to also append this separator when you eventually make requests to your  
model.  
<br>  
- Use an ending token at the end of the completion, e.g. `END`  
<br>  
- Remember to add the ending token as a stop sequence during inference,  
e.g. `stop=[" END"]`    
<br>  
- Aim for at least `~500` examples  
<br>  
- Ensure that the prompt + completion doesn't exceed `2048` tokens, including  
the separator  
<br>  
- Ensure the examples are of high quality and follow the same desired format  
<br>
- Ensure that the dataset used for finetuning is very similar in structure  
and type of task as what the model will be used for  
<br>  
- Using Lower learning rate and only `1-2` epochs tends to work better for  
these use cases

### Specific Guidelines for Classification
In classification problems, each input in the prompt should be  
classified into one of the predefined classes. For this type of problem,  
we recommend:

- Use a separator at the end of the prompt, e.g. `\n\n###\n\n`. Remember  
to also append this separator when you eventually make requests to your model.  
<br>  
- Choose classes that map to a single token. At inference time, specify  
`max_tokens=1` since you only need the first token for classification.  
<br>  
- Ensure that the prompt + completion doesn't exceed `2048` tokens, including  
the separator  
<br>
- Aim for at least `~100` examples per class  
<br>  
- To get class log probabilities you can specify `logprobs=5` (for 5  
classes) when using your model  
<br>
- Ensure that the dataset used for finetuning is very similar in  
structure and type of task as what the model will be used for
