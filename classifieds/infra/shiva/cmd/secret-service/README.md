# secret-service

Secrets delivery for nomad services

## server side
- delegation api: to store delegation tokens from users
- access api: to create access tokens for nomad-clients
- http artifacts: to deliver secrets to nomad clients artifacts

### Certificates
Certificates for server are read in PEM format with escaped newlines from environment variables
If certificates are not supplied, self-signed certificate/key pairs will be generated
