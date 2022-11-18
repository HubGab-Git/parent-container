# Parent container

## Description

Tutorial to create AWS ECR repository, create docker image with custom nginx site and push to mentioned ECR repository

## Usage

### Provision ECR

```md
aws cloudformation deploy \
--template aws/cloudFormation/ecr.yaml \
--stack-name nginx-www
```

### Create docker image

```md
docker build -t nginx-www aws/dockerFile 
```

### Docker login ECR
```md
aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.region.amazonaws.com
```

### Docker tag
```md
docker tag nginx-www:latest aws_account_id.dkr.ecr.region.amazonaws.com/softserve-nginx
```

### Docker push

```md
docker push aws_account_id.dkr.ecr.region.amazonaws.com/softserve-nginx
```

### Check if working

```md
docker run -it --rm -d -p 8080:80 --name web aws_account_id.dkr.ecr.region.amazonaws.com/softserve-nginx
```
