# Docker JupyterLab Templates
Containerized JupyterLab with Python 3
- [Available templates](#available-templates)
- [Features](#features)
- [Install requirements - Docker](#install-requirements---docker)
- [Run templates](#run-templates)
  * [Select the template of interest](#select-the-template-of-interest)
  * [Set volumes - optional](#set-volumes---optional)
  * [Start notebook](#start-notebook)
  * [Access notebook](#access-notebook)
  * [Stop notebook](#stop-notebook)
- [Ports](#ports)
# Available templates
<img src="docs/mongodb-icon.svg" alt="drawing" width="24"/> MongoDB-JupyterLab

<img src="docs/neo4j-icon.svg" alt="drawing" width="24"/> Neo4j-JupyterLab

<img src="docs/pytorch-icon.svg" alt="drawing" width="24"/> PyTorch-CUDA-JupyterLab

<img src="docs/selenium-icon.svg" alt="drawing" width="24"/> Selenium-JupyterLab

<img src="docs/apache_spark-icon.svg" alt="drawing" width="24"/> Spark-Delta-JupyterLab
# Features
:heavy_check_mark: All templates based on official images - Docker Hub

:heavy_check_mark: Code formatter - Black & isort

:heavy_check_mark: Version control - Git

:heavy_check_mark: Sync local directories
# Install requirements - Docker
## Template `PyTorch-CUDA-JupyterLab`
- Windows --> It's mandatory to install and run commands in WSL to enable GPU computing https://learn.microsoft.com/en-us/windows/wsl/install
## All templates
- Mac --> https://docs.docker.com/desktop/mac/install/
- Windows --> https://docs.docker.com/desktop/windows/install/
- Linux --> https://docs.docker.com/desktop/linux/install/
# Run templates
## Clone repository
```
git clone https://github.com/scr255/Docker-JupyterLab-Templates.git
```
## Select the template of interest
Example for template "Spark-Delta-JupyterLab":
```
cd Docker-JupyterLab-Templates/Spark-Delta-JupyterLab
```
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
```
docker compose up
```
## Access notebook
Copy token from terminal

Open http://localhost:8888/lab and paste the token

Open the .ipynb file as a starting point
## Stop notebook
Hit Ctrl+C in the terminal to stop the server

Then remove containers by submitting:
```
docker compose down
```
# Ports
All templates bind to port 8888 for Jupyter. Additional ports, depending on the template:
- MongoDB-JupyterLab --> http://localhost:8081 for Mongo Express
- Neo4j-JupyterLab --> http://localhost:7474 for Neo4j Browser
- PyTorch-CUDA-JupyterLab --> http://localhost:6006 for TensorBoard
- Spark-Delta-JupyterLab --> http://localhost:4040 for SparkUI (active task to show up)
