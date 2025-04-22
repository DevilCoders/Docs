## AWS quick start

### Получение ключей для аккаунта:

* Переходим сюда - https://console.aws.amazon.com/iam/home#/security_credentials
* Тыкаем - Access keys (access key ID and secret access key)
* Создаем ключ

### Настройка aws cli

[Ссылка на исходную доку](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)

* Скачиваем
    * Linux
      ```
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      ```
    * Mac
      ```
      curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
      sudo installer -pkg AWSCLIV2.pkg -target /
      ```
* `aws configure`

  AWS Access Key ID и AWS Secret Access Key берем из ранее созданного ключа. Default region выбираем us-east-1

## Настраиваем provider-aws

Создаем секрет

```shell
AWS_PROFILE=default && \
echo -e "[default]\naws_access_key_id = $(aws configure get aws_access_key_id --profile $AWS_PROFILE)\naws_secret_access_key = $(aws configure get aws_secret_access_key --profile $AWS_PROFILE)" > creds.conf && \
kubectl --context crossplane create secret generic aws-creds -n crossplane-system --from-file=creds=./creds.conf
```

Создаем ProviderConfig

```shell
kubectl --context crossplane apply -f infra/kube/aws/core/setup.yaml
```

## Поднимаем EKS кластер

Создаем

```
kubectl --context crossplane apply -f resource/net -f resource/eks
```

Ждем создания

```
watch kubectl --context crossplane get -f resource/net -f resource/eks
```

## Настраиваем kubectl context для EKS

```shell
aws eks --region us-east-1 update-kubeconfig --name eks --alias eks
```
