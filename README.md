# Docker JupyterLab Templates
Containerized JupyterLab with Python 3
- [Available templates](#available-templates)
- [Features](#features)
- [Install requirements - Docker](#install-requirements---docker)
- [Run templates](#run-templates)
  * [Select template of interest](#select-template-of-interest)
  * [Set shared memory - optional](#set-shared-memory---optional)
  * [Set volumes - optional](#set-volumes---optional)
  * [Start notebook](#start-notebook)
  * [Access notebook](#access-notebook)
  * [Stop notebook](#stop-notebook)
- [Ports](#ports)
# Available templates
<img src="docs/mongodb-icon.svg" alt="drawing" width="24"/> MongoDB-JupyterLab

<img src="docs/neo4j-icon.svg" alt="drawing" width="24"/> Neo4j-JupyterLab

<img src="docs/pytorch-icon.svg" alt="drawing" width="24"/> PyTorch-CPU-JupyterLab

<img src="docs/pytorch-icon.svg" alt="drawing" width="24"/> PyTorch-CUDA-JupyterLab

<img src="docs/selenium-icon.svg" alt="drawing" width="24"/> Selenium-JupyterLab

<img src="docs/apache_spark-icon.svg" alt="drawing" width="24"/> Spark-Delta-JupyterLab
# Features
:heavy_check_mark: All templates based on official images - Docker Hub

:heavy_check_mark: Code formatter - black & isort

:heavy_check_mark: Version control - Git

:heavy_check_mark: Volumes binded from local directory
# Install requirements - Docker
## All templates but `PyTorch-CUDA-JupyterLab`
- Mac --> https://docs.docker.com/desktop/mac/install/
- Windows --> https://docs.docker.com/desktop/windows/install/
- Linux --> https://docs.docker.com/desktop/linux/install/
## Template `PyTorch-CUDA-JupyterLab`
- Windows --> In order to enable GPU computing, it's mandatory to use WSL https://docs.nvidia.com/cuda/wsl-user-guide/index.html#getting-started-with-cuda-on-wsl
- Linux (and WSL) --> https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#getting-started
# Run templates
## Select template of interest
Example for template "Spark-Delta-JupyterLab":
```
git clone https://github.com/scr255/Docker-JupyterLab-Templates.git
cd Docker-JupyterLab-Templates/Spark-Delta-JupyterLab
```
## Set shared memory - optional
Default is 8gb on most templates, edit "docker-compose.yml" if necessary:
```
    shm_size: '16gb'
```
(delete this line for default shared memory)
## Set volumes - optional
### Default sync based on current directory:
```
    volumes:
      - .:/home/jovyan/work
```
### Sync specific path by editing "docker-compose.yml":
```
    volumes:
      - ~/Documents:/home/jovyan/work
```
## Start notebook
### All templates but `MongoDB-JupyterLab`
```
docker compose up
```
### Template `MongoDB-JupyterLab`
Create volume and start notebook:
```
docker volume create mongo_external
docker compose up --attach mongodb-lab
```
("--attach mongodb-lab" reduces logging from MongoDB)
## Access notebook
Copy token from terminal

Open http://localhost:8888/lab and paste token

Open the .ipynb file as starting point
## Stop notebook
Hit Ctrl+C in terminal to stop server

Then remove containers by submitting:
```
docker compose down
```
# Ports
All templates bind port 8888 for Jupyter. Additional ports, depending on template:
- MongoDB-JupyterLab --> http://localhost:8081 for Mongo Express
- Neo4j-JupyterLab --> http://localhost:7474 for Neo4j Browser
- PyTorch-CPU-JupyterLab --> http://localhost:6006 for TensorBoard
- PyTorch-CUDA-JupyterLab --> http://localhost:6006 for TensorBoard
- Spark-Delta-JupyterLab --> http://localhost:4040 for SparkUI (need active task to show up)
