# Groq 

## Connection to Groq

![Groq connection diagram](./groqrack_system_diagram.png)

Login to the Groq login node from your local machine.
Once you are on the login node, ssh to one of the Groq nodes.

```bash
local > ssh ALCFUserID@groq.ai.alcf.anl.gov
```
```bash
groq-login > ssh groq-r01-gn-01.ai.alcf.anl.gov
# or
groq-login > ssh groq-r01-gn-09.ai.alcf.anl.gov
# or any node with hostname of form groq-r01-gn-0[1-9].ai.alcf.anl.gov
```

## Prerequisite: Create Virtual Environment 

### Install Miniconda

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

### PyTorch virtual environment

```bash
export PYTHON_VERSION=3.10.12
conda create -n groqflow python=$PYTHON_VERSION -y
conda activate groqflow
```

### Install Groqflow

```bash
# Alter this if you have cloned groqflow to some other location.
cd ~/groqflow
if [ -d "groqflow.egg-info" ]; then rm -r groqflow.egg-info; fi
pip install --upgrade pip
pip list --format=freeze > frozen.txt
pip install -r frozen.txt -e .
pushd . 
cd demo_helpers
if [ -d "groqflow_demo_helpers.egg-info" ]; then rm -r groqflow_demo_helpers.egg-info; fi
pip install -e .
popd
pip install soundfile
```

### Use GroqFlow
```bash
conda activate groqflow
```

## Job Queuing and Submission

Groq jobs in the AI Testbed's Groqrack are managed by the PBS job scheduler.

* `qsub` : to submit a batch job using a script
* `qstat`: to display queue information
* `qdel`: to delete (cancel) a job:
* `qhold`: to hold a job

<!-- ### Schedule batch Job

<details>
  <summary>Sample run_minilmv2.sh script</summary>
  
    ```bash
    #!/bin/bash
    # >>> conda initialize >>>
    # !! Contents within this block are managed by 'conda init' !!
    __conda_setup="$(${HOME}'/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
    if [ $? -eq 0 ]; then
        eval "$__conda_setup"
    else
        if [ -f "${HOME}/miniconda3/etc/profile.d/conda.sh" ]; then
            . "${HOME}/miniconda3/etc/profile.d/conda.sh"
        else
            export PATH="${HOME}/miniconda3/bin:$PATH"
        fi
    fi
    unset __conda_setup
    # <<< conda initialize <<<
    conda activate groqflow
    cd ~/groqflow/proof_points/natural_language_processing/minilm
    pip install -r requirements.txt
    python minilmv2.py

    ```
    
</details>

Then run the script as a batch job with PBS:
```bash
qsub run_minilmv2.sh
``` -->


### Schedule Interactive Job

Following command gives a single Groq node interactively for 1 hour
```bash
qsub -I -l walltime=1:00:00 
```
Other flags that can be used
```bash
-l ncpus=1 
-l groq_accelerator=1
```

## Hands-on Example


* [Bert](./bert.md)

## Homework

Run BERT example with custom input instead of dummy input. 

I used a max sequence length of 256 instead of 128: 

(groqflow) saideepgona@groq-r01-gn-08:~/groqflow/proof_points/natural_language_processing/bert$ python bert_tiny.py         
/home/saideepgona/miniconda3/envs/groqflow/lib/python3.10/site-packages/torch/_utils.py:831: UserWarning: TypedStorage is deprecated. It will be removed in the future and UntypedStorage will be the only storage class. This should only matter to you if you are using storages directly.  To access UntypedStorage directly, use tensor.untyped_storage() instead of tensor.storage()
  return self.fget.__get__(instance, owner)()

Warning: build_model() discovered a cached build of bert_tiny, but decided to rebuild for the following reasons: 
         
         - Input shape of model "bert_tiny" changed from {'attention_mask': (1, 128), 'input_ids': (1, 128)} to {'attention_mask': (1, 256), 'input_ids': (1, 256)} since the last time it was built. 
         
         build_model() will now rebuild your model to ensure correctness. You can change this policy by setting the build_model(rebuild=...) argument.



Building "bert_tiny"
    ✓ Exporting PyTorch to ONNX   
    ✓ Optimizing ONNX file   
    ✓ Checking for Op support   
    ✓ Converting to FP16   
    ✓ Compiling model   
    ✓ Assembling model   

Woohoo! Saved to ~/.cache/groqflow/bert_tiny
Preprocessing data.
/home/saideepgona/miniconda3/envs/groqflow/lib/python3.10/site-packages/datasets/load.py:1461: FutureWarning: The repository for sst contains custom code which must be executed to correctly load the dataset. You can inspect the repository content at https://hf.co/datasets/sst
You can avoid this message in future by passing the argument `trust_remote_code=True`.
Passing `trust_remote_code=True` will be mandatory to load this dataset from the next major release of `datasets`.
  warnings.warn(

Info: No inputs received for benchmark. Using the inputs provided during model compilation.
Running inference on GroqChip.
Running inference using PyTorch model (CPU).
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2210/2210 [00:09<00:00, 245.13it/s]
+--------+----------+-------------------------+----------------+----------------------+-------------+
| Source | Accuracy | end-to-end latency (ms) | end-to-end IPS | on-chip latency (ms) | on-chip IPS |
+--------+----------+-------------------------+----------------+----------------------+-------------+
|  cpu   |  77.47%  |           4.08          |     245.05     |          --          |      --     |
|  groq  |  77.47%  |           0.07          |    14107.26    |         0.04         |   23391.20  |
+--------+----------+-------------------------+----------------+----------------------+-------------+
Proof point /home/saideepgona/groqflow/proof_points/natural_language_processing/bert/bert_tiny.py finished!



## Additional Examples (Optional)

* [ResNet50](./resnet50.md)
* [MiniLMv2](./minilm.md)
<!-- * * [GPT2](./gpt2.md) -->

## Useful Resources 

* [ALCF Groq Documenation](https://docs.alcf.anl.gov/ai-testbed/groq/system-overview/)
* [Groq Documentation](https://support.groq.com/#/login)
* [Groq Examples Repository](https://github.com/groq/groqflow/tree/main/proof_points)

