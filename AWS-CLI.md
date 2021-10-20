# AWS CLI 설치 & 설정

## 1. CLI v2 설치

```bash
$ sudo apt install unzip
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install
$ aws --version
```

## 2. 설정

- 엑세스 키와 비밀 키는 IAM 에서 생성
- 서울 리전 : ap-northeast-2

```bash
$ aws configure
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]: ap-northeast-2
Default output format [None]: yaml
```

## 참고 자료

- [Installing, updating, and uninstalling the AWS CLI version 2 on Linux](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html)
- [Configuration basics](​https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
