# Cerebras 

## Connection to a CS-2 node

Connection to one of the CS-2 cluster login nodes requires an MFA passcode for authentication - either an 8-digit passcode generated by an app on your mobile device (e.g. MobilePASS+) or a CRYPTOCard-generated passcode prefixed by a 4-digit pin. This is the same passcode used to authenticate into other ALCF systems, such as Theta and Cooley.

![CS-2 connection diagram](./Cerebras_Wafer-Scale_Cluster_login_diagram.png)

To connect to a CS-2 login, ssh to login nodes:
```bash
ssh ALCFUserID@cerebras.ai.alcf.anl.gov
```

## Prerequisite: Create Virtual Environment 

### PyTorch virtual environment

```bash
#Make your home directory navigable
chmod a+xr ~/
mkdir ~/R_2.1.1
chmod a+x ~/R_2.1.1/
cd ~/R_2.1.1
# Note: "deactivate" does not actually work in scripts.
deactivate
rm -r venv_cerebras_pt
/software/cerebras/python3.8/bin/python3.8 -m venv venv_cerebras_pt
source venv_cerebras_pt/bin/activate
pip install --upgrade pip
pip install cerebras_pytorch==2.1.1
```

## Clone Cerebras modelzoo

We use an example from [Cerebras Modelzoo repository](https://github.com/Cerebras/modelzoo) for this hands-on. 

* Clone the modezoo repository.<br>
```bash
mkdir ~/R_2.1.1
cd ~/R_2.1.1
git clone https://github.com/Cerebras/modelzoo.git
cd modelzoo
git tag
git checkout Release_2.1.1    
```
* Install requirements for modelzoo
    ```bash
    cd ~/R_2.1.1/modelzoo
    pip install -r requirements.txt 
    ```

## Job Queuing and Submission

The CS-2 cluster has its own Kubernetes-based system for job submission and queuing. Jobs are started automatically through the Python scripts. 

Use Cerebras cluster command line tool to get addional information about the jobs.

* Jobs that have not yet completed can be listed as
    `(venv_pt) $ csctl get jobs`
* Jobs can be canceled as shown:
    `(venv_tf) $ csctl cancel job wsjob-eyjapwgnycahq9tus4w7id`

See `csctl -h` for more options.

## Hands-on Example

* [BERT](./bert-large.md)

## Homework

Run BERT example with different batch sizes like 512, 2048 and observe the performance difference.  

Batch size 512:

Beginning appliance run
| Train Device=CSX, Step=100, Loss=9.39062, Rate=2997.12 samples/sec, GlobalRate=2997.12 samples/sec
| Train Device=CSX, Step=200, Loss=8.70312, Rate=2952.14 samples/sec, GlobalRate=2959.16 samples/sec
| Train Device=CSX, Step=300, Loss=7.79688, Rate=2937.27 samples/sec, GlobalRate=2948.48 samples/sec
| Train Device=CSX, Step=400, Loss=7.39062, Rate=2925.75 samples/sec, GlobalRate=2940.82 samples/sec
| Train Device=CSX, Step=500, Loss=7.80469, Rate=2926.62 samples/sec, GlobalRate=2938.08 samples/sec
| Train Device=CSX, Step=600, Loss=7.53125, Rate=2911.71 samples/sec, GlobalRate=2931.97 samples/sec
| Train Device=CSX, Step=700, Loss=7.35156, Rate=2909.51 samples/sec, GlobalRate=2928.53 samples/sec
| Train Device=CSX, Step=800, Loss=7.27344, Rate=2907.21 samples/sec, GlobalRate=2925.65 samples/sec
| Train Device=CSX, Step=900, Loss=7.35938, Rate=2916.78 samples/sec, GlobalRate=2925.37 samples/sec
| Train Device=CSX, Step=1000, Loss=7.12500, Rate=2905.80 samples/sec, GlobalRate=2922.66 samples/sec

Batch size 2048:

Beginning appliance run
| Train Device=CSX, Step=100, Loss=9.48438, Rate=6781.68 samples/sec, GlobalRate=6781.69 samples/sec
| Train Device=CSX, Step=200, Loss=8.48438, Rate=6765.25 samples/sec, GlobalRate=6767.96 samples/sec
| Train Device=CSX, Step=300, Loss=7.77344, Rate=6695.69 samples/sec, GlobalRate=6727.95 samples/sec
| Train Device=CSX, Step=400, Loss=7.64062, Rate=6710.88 samples/sec, GlobalRate=6726.21 samples/sec
| Train Device=CSX, Step=500, Loss=7.37500, Rate=6730.82 samples/sec, GlobalRate=6729.78 samples/sec
| Train Device=CSX, Step=600, Loss=7.42188, Rate=6749.89 samples/sec, GlobalRate=6735.23 samples/sec
| Train Device=CSX, Step=700, Loss=7.25000, Rate=6754.49 samples/sec, GlobalRate=6738.41 samples/sec
| Train Device=CSX, Step=800, Loss=7.12500, Rate=6739.56 samples/sec, GlobalRate=6737.31 samples/sec
| Train Device=CSX, Step=900, Loss=7.25000, Rate=6744.52 samples/sec, GlobalRate=6738.48 samples/sec
| Train Device=CSX, Step=1000, Loss=7.14844, Rate=6749.38 samples/sec, GlobalRate=6739.89 samples/sec


It seems like increasing the batch size from 512 to 2048 doesn't have too much of an effect on the training loss, although the rate of learning increases nearly 3-fold. 


### Additional Examples (Optional)

* [GPT-J](./gptj.md)
* [GPT-2](./gpt2.md)

# Useful Resources 

* [ALCF Cerebras Documentation](https://docs.alcf.anl.gov/ai-testbed/cerebras/system-overview/)
* [Cerebras Documntation](https://docs.cerebras.net/en/latest/wsc/index.html)
* [Cerebras Modelzoo Repo](https://github.com/Cerebras/modelzoo/tree/main/modelzoo)
* Datasets Path: `/software/cerebras/dataset`
