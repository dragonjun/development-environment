# development-environment

Windows Subsystem for Linux (WSL) & Ubuntu

- [Zsh](#Zsh)
- [AWS CLI](#aws-cli)
- [kubectl](#kubectl)
- [Helm](#helm)

## Zsh

- [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- [romkatv/powerlevel10k: A Zsh theme](https://github.com/romkatv/powerlevel10k)
- [powerline/fonts: Patched fonts for Powerline users.](https://github.com/powerline/fonts)
- [ryanoasis/nerd-fonts: Iconic font aggregator, collection, & patcher.](https://github.com/ryanoasis/nerd-fonts)

1. Zsh
   ```bash
   $ sudo apt update && sudo apt upgrade -y
   $ sudo apt install zsh -y
   $ zsh --version
   $ sudo chsh -s $(which zsh) $(whoami)
   ```
2. Oh My Zsh
   ```bash
   $ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
   ```
3. Powerlevel10k
   ```bash
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   ```
4. zsh-autosuggestions & zsh-syntax-highlighting
   ```bash
   $ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   $ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```
5. `~/.zshrc` 수정

   `ZSH_THEME="powerlevel10k/powerlevel10k"`
   `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`

   ```bash
   $ sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc
   $ sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc
   $ exit
   ```

## AWS CLI

- [AWS CLI Installing](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [AWS CLI Command completion](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html)
- [AWS CLI Configuration basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)

```bash
$ sudo apt install unzip
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install
$ aws --version
$ echo -e "\n# AWS CLI Command completion" >>~/.zshrc
$ echo "autoload bashcompinit && bashcompinit" >>~/.zshrc
$ echo "autoload -Uz compinit && compinit" >>~/.zshrc
$ echo "complete -C '/usr/local/bin/aws_completer' aws" >>~/.zshrc
$ source ~/.zshrc

$ aws configure
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]: ap-northeast-2
Default output format [None]: json

$ aws configure list
```

## kubectl

- [Installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)
- [kubectl zsh auto-completion](https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-zsh/)

```bash
$ curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$ mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
$ kubectl version --short --client
$ echo -e '\nexport PATH=$PATH:$HOME/bin' >> ~/.zshrc
$ echo -e '\n# Kubernetes auto completion' >>~/.zshrc
$ echo 'source <(kubectl completion zsh)' >>~/.zshrc
$ echo 'alias k=kubectl' >>~/.zshrc
$ echo 'complete -F __start_kubectl k' >>~/.zshrc
$ source ~/.zshrc

$ aws sts get-caller-identity
$ aws eks update-kubeconfig --name <cluster-name> --alias <context-name>
$ kubectl get svc
```

## Helm

- [Helm](https://helm.sh/)
- [Helm | Installing Helm](https://helm.sh/docs/intro/install/)

```bash
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
$ echo -e '\n# Helm auto completion' >>~/.zshrc
$ echo 'source <(helm completion zsh)' >>~/.zshrc
$ source ~/.zshrc
```
