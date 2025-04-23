# Gitlab Community

## AWS installation bootstrap on EC2 instance

// TODO: provision installation via crossplane/terraform?

1. Create VPC with public subntes (with NAT).
2. Set 'Enable auto-assign public IPv4 address' option for public subnets
3. Import your ssh-key in EC2 key pair:

```shell
aws ec2 import-key-pair --key-name "vaspahomov-yandex" --public-key-material fileb://~/.ssh/id_rsa.pub
```

5. Open [Gitlab on AWS page](https://about.gitlab.com/partners/technology-partners/aws/) and follow instructions

Use subnets created on previous steps. Use keypair imported on last step.

6. ssh to created EC2 instance
7. Reset root password:

```shell
sudo gitlab-rake "gitlab:password:reset[root]"
```

8. Now you can login in your gitlab installation as root user
   (use `username=root, password='<your-password-after-reset>'`). All other user registration should be approved by
   administrator.

### TODO:

* How to setup integration with AWS IAM?
