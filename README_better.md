## Access quest

Location of repo on quest:
```
/projects/b1196/ewa_group/condot/
```

### Setup of notebook on GPU

First:
- connect to quest
- get on gpu in screen
- load `conda activate /projects/b1196/envs/condot`
- run jupyter lab `jupyter-lab --port 4321` 

### Sharing (is caring) a jupyter-lab

**To share**

In new window:
- connect to quest
- get `<ip>` with ifconfig (first one after inet)
- run screen
- run `ssh -4 -L4311:localhost:8888 gpu_node`

**To receive**

Locally:
`ssh -L8888:localhost:4321<netid>@<ip>`


## Installation



Prepare environment:

```
eval "$(/software/mamba/23.1.0/bin/conda shell.bash hook)"
CONDA_OVERRIDE_CUDA="11.2" mamba create --prefix=/projects/b1196/envs/condot -c conda-forge gxx_linux-64 gcc_linux-64 python=3.9.7 cudatoolkit=11.2
conda activate /projects/b1196/envs/condot
pip install pip-tools
```

Install condot:

```
cd /projects/b1196/ewa_group/condot/
pip-compile requirements.in
pip-sync
python setup.py develop
```

Every new dependency should be added first to `requirements.in`, then:
```
pip-compile requirements.in
pip-sync
python setup.py develop
```
It will take a while to resolve the dependencies. No `pip install` for the sake of sanity :( 

```
screen -S condot
# Run GPU here
conda activate /projects/b1196/envs/condot
cd /projects/b1196/ewa_group/condot/
```