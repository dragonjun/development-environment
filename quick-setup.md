# development-environment

Windows Subsystem for Linux (WSL) & Ubuntu

- Zsh
- Oh My Zsh
- zsh-autosuggestions
- zsh-syntax-highlighting
- Powerlevel10k
- AWS CLI
- kubectl
- Helm

## Quick Setup

### Step 1

```bash
$ mkdir temp && cd temp && \
  sudo apt update && sudo apt upgrade -y && \
  sudo apt install zsh -y && \
  zsh --version && \
  sudo chsh -s $(which zsh) $(whoami) && \
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended && \
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && \
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && \
  sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc && \
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k && \
  sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc && \
  sudo apt install unzip && \
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
  unzip awscliv2.zip && \
  sudo ./aws/install && \
  aws --version && \
  echo -e "\n# AWS CLI Command completion" >>~/.zshrc && \
  echo "autoload bashcompinit && bashcompinit" >>~/.zshrc && \
  echo "autoload -Uz compinit && compinit" >>~/.zshrc && \
  echo "complete -C '/usr/local/bin/aws_completer' aws" >>~/.zshrc && \
  curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl && \
  chmod +x ./kubectl && \
  mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin && \
  kubectl version --short --client && \
  echo -e '\nexport PATH=$PATH:$HOME/bin' >> ~/.zshrc && \
  echo -e '\n# Kubernetes auto completion' >>~/.zshrc && \
  echo 'source <(kubectl completion zsh)' >>~/.zshrc && \
  echo 'alias k=kubectl' >>~/.zshrc && \
  echo 'complete -F __start_kubectl k' >>~/.zshrc && \
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 && \
  chmod 700 get_helm.sh && \
  ./get_helm.sh && \
  echo -e '\n# Helm auto completion' >>~/.zshrc && \
  echo 'source <(helm completion zsh)' >>~/.zshrc && \
  cd ~
```

```bash
exit
```

### Step 2

```bash
$ aws configure
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]: ap-northeast-2
Default output format [None]: json

$ aws configure list

$ aws --no-cli-pager sts get-caller-identity && \
  aws eks update-kubeconfig --region ap-northeast-2 --name sunnyvale --verbose --alias sunnyvale && \
  kubectl get svc
```
