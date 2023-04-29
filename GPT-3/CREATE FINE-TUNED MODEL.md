# Create a Fine-Tuned Model
The following assumes you've already prepared training data following  
the instructions in [this](TRAINING%20DATA.md) document.  
<br>  
Start your fine-tuning job using the `OpenAI CLI`:
> openai api fine_tunes.create -t <TRAIN_FILE_ID_OR_PATH> -m <BASE_MODEL>

where `BASE_MODEL` is the name of the base model you're starting from   
(ada, babbage, curie, or davinci). Your can customize your fine-tuned  
models' name using the suffix parameter:
> openai api fine_tunes.create -t <TRAIN_FILE_ID_OR_PATH> -m <BASE_MODEL> --suffix "custom model name"  

Running the above command does several things:
1. Uploads the files that will be used for fine-tuning using [files API](https://platform.openai.com/docs/api-reference/files)  
(or uses an already-uploaded file) 
2. Creates a fine-tune job
3. Streams events until the job is done (this often takes minutes, but  
can take hours if there are many jobs in the queue or your dataset is  
large)

Every fine-tuning job starts from a base model, which defaults to `curie`.  
The choice of model influences both the performance of the model and   
the cose of running your fine-tuned model.
<br>  
After you've started a fine-tune job, it may take some time to complete.  
Your job may be queued behind other jobs on the OpenAI' system, and  
training the model can take minutes of hours depending on the model and  
dataset size. If the event stream is interrupted for any reason, you can   
resume it by running:
> openai api fine_tunes.follow -i <YOUR_FINE_TUNE_JOB_ID>

When the job is done, it should display the name of the fine-tuned model.  
<br>
In addition to creating a fine-tune job, you can also list existing jobs,  
retrieve the status of a job, or cancel a job.
> #&#8203; List all created fine-tunes    
> openai api fine_tunes.list  
>   
> #&#8203; Retrieve the state of a fine-tune. The resulting object includes  
> #&#8203; job status (which can be one of pending, running, succeeded, or failed)  
> #&#8203; and other information  
> openai api fine_tunes.get -i <YOUR_FINE_TUNE_JOB_ID>  
>   
> #&#8203; Cancel a job  
> openai api fine_tunes.cancel -i <YOUR_FINE_TUNE_JOB_ID>  

