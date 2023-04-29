# Use a Fine-Tuned Model
The following assumes you've already fine-tuned your model following    
the instructions in [this](CREATE%20FINE-TUNED%20MODEL.md) document.  
<br>  
When a fine-tuning job has succeeded, the `fine_tuned_model` field will  
be populated with the name of the model. You may now specify this model  
as a parameter to [Completions API](https://platform.openai.com/docs/api-reference/completions), and make requests to is using the  
[Playground](https://platform.openai.com/playground).  
<br> 
After your fine-tuning job first completes, it may take several minutes  
for your model to become ready to handle requests. If completion requests  
to your model time out, it is likely because your model is still being  
loaded. If this happens, try again in a few minutes.   
<br>
You can start making requests by passing the model name as the `model`  
parameter of a completion request:
### OpenAI CLI:
> openai api completions.create -m <FINE_TUNED_MODEL> -p <YOUR_PROMPT>


### cURL:
> curl https://api.openai.com/v1/completions \    
> -H "Authorization: Bearer $OPENAI_API_KEY" \    
> -H "Content-Type: application/json" \  
> -d '{"prompt": YOUR_PROMPT, "model": FINE_TUNED_MODEL}'  


### Python:
> import openai  
> openai.Completion.create(  
> &emsp;&emsp;model=FINE_TUNED_MODEL,  
> &emsp;&emsp;prompt=YOUR_PROMPT)  
