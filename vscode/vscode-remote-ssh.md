# VS Code Remote Development

## Remote Development using SSH

1. [OpenSSH](https://docs.microsoft.com/ko-kr/windows-server/administration/openssh/openssh_install_firstuse) 설치
1. [Remote Development Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) 설치

### Private key file permission 수정

PowerShell 에서 다음 커맨드 실행

```ps1
$path = "C:\keys\private-key.pem"
# Reset to remove explict permissions
icacls.exe $path /reset
# Give current user explicit read-permission
icacls.exe $path /GRANT:R "$($env:USERNAME):(R)"
# Disable inheritance and remove inherited permissions
icacls.exe $path /inheritance:r

$destination = "ubuntu@10.0.0.1"
ssh -i $path $destination
```

### PowerShell 에서 접속

```ps1
$path = "C:\keys\private-key.pem"
$destination = "ubuntu@10.0.0.1"
ssh -i $path $destination
```

### VS Code 에서 서버 설정

1. Command Palette (Ctrl+Shift+P)
1. Remote-SSH: Open Configuration File...
1. C:\Users\user-name\.ssh\config 선택

다음과 같이 입력하고 저장

```
Host name-of-ssh-host-here
    HostName host-fqdn-or-ip-goes-here
    User your-user-name-on-host
    IdentityFile private-key-file-path
```

### VS Code 에서 접속

1. Command Palette (Ctrl+Shift+P)
1. Remote-SSH: Connect to Host...

---

- [Remote Development using SSH](https://code.visualstudio.com/docs/remote/ssh)
- [Amazon EC2 key pairs and Linux instances - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
- [Connect to your Linux instance using an SSH client](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
