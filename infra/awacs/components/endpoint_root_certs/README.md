ENDPOINT_ROOT_CERTS
========

ENDPOINT_ROOT_CERTS component is building from the following pems:

###### Yandex Internal CAs

* YandexInternalCA.pem
* YandexInternalRootCA.pem

From: https://crls.yandex.net/allCAs.pem

###### Certum Trusted Network Certification Authority

* CertumTrustedNetworkCA.pem
* CertumTrustedNetworkCA2.pem

From: https://www.certum.eu/en/cert_expertise_root_certificates/

###### GlobalSign

RSA
* GlobalSign Root CA
* GlobalSign Root CA - R3
* GlobalSign Root CA - R6
* GlobalSign Root R46

ECC
* GlobalSign ECC Root CA - R5
* GlobalSign Root E46

From: https://support.globalsign.com/ca-certificates/root-certificates/globalsign-root-certificates

##### How to build

```
cat YandexInternalCA.pem YandexInternalRootCA.pem CertumTrustedNetworkCA.pem CertumTrustedNetworkCA2.pem GlobalSignRootCA.pem GlobalSignRootCA_R3.pem GlobalSignRootCA_R6.pem GlobalSignRoot_R46.pem GlobalSignECCRootCA_R5.pem GlobalSignECCRoot_E46.pem | /home/linuxbrew/.linuxbrew/Cellar/cif/1.1.0/bin/cif > allCAs.pem
```

We are using cif from https://github.com/gesquive/cif to annotate base64 with human-readable description
