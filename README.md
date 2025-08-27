# CancerLLM
Cancer LLM platform for target discovery and drug development

# Software
- MacMini
- Docker
- AWS CLI

```
sudo installer -pkg AWSCLIV2.pkg -target /
aws --version
aws configure
aws s3 ls
```

# logic flow
1. creat a docker image in MacMini; [fail to build from DockFile, issue: no access to conda channels]

```
docker pull mambaorg/micromamba:1.5.8 # pull a pre-built image

apt update && apt install -y git curl bzip2 vim iputils-ping curl # install basic tools

apt update && apt install -y ca-certificates
update-ca-certificates

# https://github.com/snap-stanford/Biomni/blob/main/biomni_env/README.md
git clone https://github.com/snap-stanford/Biomni.git
cd Biomni/biomni_env

vi biomni.environment.yml # modify the channels

micromamba create -y -n biomni_e1 -f biomni.environment.yml # use micromamba, no conda pre-installed

micromamba activate biomni_e1

# download files [will delete this later]
from biomni.agent import A1
# Initialize the agent with data path, Data lake will be automatically downloaded on first run (~11GB)
agent = A1(path='./data', llm='claude-sonnet-4-20250514')
# Execute biomedical tasks using natural language
agent.go("Plan a CRISPR screen to identify genes that regulate T cell exhaustion, generate 32 genes that maximize the perturbation effect.")

exit

docker commit biomni-debug biomni-image:latest
```

modify `docker-compose.yml`, then start `docker compose up -d`, open http://localhost/web/index.html 
```
services:
  biomni:
    image: biomni-image:latest
    container_name: biomni
    restart: unless-stopped
    ports:
      - "8000:8000"
    volumes:
      - ./data:/data
```

```
# Don't use mirrors.ustc.edu.cn, no response. Use mirrors.tuna.tsinghua.edu.cn. 2025-Aug-26
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
```

# Debug
```
# check if docker is running
docker ps

# go into the running docker image, check if the local biomin is running correctly.
docker exec -it biomni bash
micromamba activate biomni_e1
python # be aware of the location of data folder

from biomni.agent import A1
# Initialize the agent with data path, Data lake will be automatically downloaded on first run (~11GB)
agent = A1(path='./data', llm='claude-sonnet-4-20250514')
agent = A1(path='./data', llm='llama2', source="Ollama", base_url="http://host.docker.internal:11434/v1")

agent.go("Predict ADMET properties for this compound: CC(C)CC1=CC=C(C=C1)C(C)C(=O)O")
```

Start: ./start.sh
Stop: docker stop biomni nginx
View logs: docker logs biomni

curl http://localhost:11434/api/generate -d '{
  "model": "llama2",
  "prompt": "Hello from Biomni!"
}'

curl http://host.docker.internal:11434/api/generate -d '{
  "model": "llama2",
  "prompt": "Hello from Biomni!"
}'
