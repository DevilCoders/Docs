# extdata-serverless
serverless functions monorepo, but pls no shared modules
# develop
copy sa_name.json / CA.pem to function project root, to support ydb connectivity
# deploy
run ```./build.sh <func-dir>``` then drop ./<func-dir>.zip in cloud console editor