# SSH

```bash
ssh -i /path/my-key-pair.pem my-instance-user-name@my-instance-public-dns-name
ssh kubectl
```

````
# ~/.ssh/config
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
Host kubectl
    HostName ec2-3-35-177-127.ap-northeast-2.compute.amazonaws.com
    User ubuntu
    IdentityFile ~/aws/web-server.pem

Host *
    ServerAliveInterval 240
    ServerAliveCountMax 2
```

---

## References

- [General prerequisites for connecting to your instance - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html)
- [Connect to your Linux instance using SSH - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
````
