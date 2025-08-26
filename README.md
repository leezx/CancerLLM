# CancerLLM
Cancer LLM platform for target discovery and drug development

# Software
- MacMini
- Docker
- AWS CLI `aws --version`

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
```

# don't use mirrors.ustc.edu.cn, no response. Use mirrors.tuna.tsinghua.edu.cn. 2025-Aug-26
```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
```
