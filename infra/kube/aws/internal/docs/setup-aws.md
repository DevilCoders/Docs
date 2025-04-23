# EKS quick start

## Логинимся в ui AWS

### Логин через SSO

TODO: написать инструкцию, когда настроим SSO

### Логин как root user

1. Заходим на https://console.aws.amazon.com
2. Выбираем радиокнопку "Root user"
3. В "Root user email address" вводим имя аккаунта, который нам создали в Capacity planning
4. Переходим дальше, пробираемся через капчи
5. В "Password" вводим пароль, который нам выдали в Capacity planning

## Инструменты

Для работы нам потребуется:

* kubectl - наш основной рабочий инструмент для работы с kubernetes. Установить можно
  следуя [официальной инструкции](https://kubernetes.io/docs/tasks/tools/#kubectl).
* aws-cli - консольный интерфейс управления ресурсами aws. Для установки:
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

## Настраиваем aws-cli профиль для работы с нужным аккаунтом

* Переходим сюда - https://console.aws.amazon.com/iam/home#/security_credentials
* Тыкаем - Access keys (access key ID and secret access key)
* Создаем ключ

* `aws configure`

  AWS Access Key ID и AWS Secret Access Key берем из ранее созданного ключа. Default region выбираем us-east-1

## Настраиваем kubectl context для EKS

```shell
aws eks --region us-east-1 update-kubeconfig --name eks --alias eks
```

## Проверяем корректность настройки kubectl

```shell
kubectl --context eks api-resources
```

Команда должна вывести список доступных ресурсов в k8s.
