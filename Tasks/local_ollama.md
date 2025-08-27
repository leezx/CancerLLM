
# install without root

curl -L https://ollama.com/download/ollama-linux-arm64.tgz -o ollama-linux-arm64.tgz

mkdir -p ~/.local
tar -C ~/.local -xzf ollama-linux-arm64.tgz

ollama serve &
ollama run llama2

Couldn't find '/home/zz950/.ollama/id_ed25519'. Generating new private key.
Your new public key is:
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDPWgYDsY9YF44PCKFjAbQiSJwsJlKVHVmAecrCvxhhE

/exit
