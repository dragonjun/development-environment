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
- Terraform

## Quick Setup

### Step 1

```bash
$ mkdir temp && cd temp && \
  sudo apt install zsh -y && \
  zsh --version && \
  sudo chsh -s $(which zsh) $(whoami) && \
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended && \
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && \
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && \
  sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc && \
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k && \
  sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc && \
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
  unzip -u awscliv2.zip && \
  sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update && \
  aws --version && \
  echo -e "\n# AWS CLI Command completion" >>~/.zshrc && \
  echo "autoload bashcompinit && bashcompinit" >>~/.zshrc && \
  echo "autoload -Uz compinit && compinit" >>~/.zshrc && \
  echo "complete -C '/usr/local/bin/aws_completer' aws" >>~/.zshrc && \
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
  curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" && \
  echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check && \
  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
  kubectl version --client && \
  echo -e '\nexport PATH=$PATH:$HOME/bin' >> ~/.zshrc && \
  echo -e '\n# Kubernetes auto completion' >>~/.zshrc && \
  echo 'source <(kubectl completion zsh)' >>~/.zshrc && \
  echo 'alias k=kubectl' >>~/.zshrc && \
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 && \
  chmod 700 get_helm.sh && \
  ./get_helm.sh && \
  echo -e '\n# Helm auto completion' >>~/.zshrc && \
  echo 'source <(helm completion zsh)' >>~/.zshrc && \
  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list && \
  sudo apt update && sudo apt install terraform && \
  echo -e '\n# Terraform auto completion' >>~/.zshrc && \
  terraform -install-autocomplete && \
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

---

- [Installing ZSH · ohmyzsh/ohmyzsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)
- [GitHub - ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)
- [zsh-users/zsh-autosuggestions: Fish-like autosuggestions for zsh](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-users/zsh-syntax-highlighting: Fish shell like syntax highlighting for Zsh.](https://github.com/zsh-users/zsh-syntax-highlighting)
- [romkatv/powerlevel10k: A Zsh theme](https://github.com/romkatv/powerlevel10k)
- [Install or update the latest version of the AWS CLI - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [Command completion - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html)
- [Install and Set Up kubectl on Linux | Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [Helm | Installing Helm](https://helm.sh/docs/intro/install/)
- [Helm | Helm Completion Zsh](https://helm.sh/docs/helm/helm_completion_zsh/)
- [Install | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/downloads)
- [Basic CLI Features | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/cli/commands#shell-tab-completion)
