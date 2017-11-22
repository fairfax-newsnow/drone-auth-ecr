# drone-auth-ecr
Customised drone plugin which can be used to pull ECR images in aws.

# public image

https://hub.docker.com/r/newsnowio/drone-auth-ecr/

### Build the image

```
# Make sure you have login docker account
$ docker login -u newsnowio

# Build and push the image (tag is latest)
$ ./build.sh

# manually tag the image, such as 1.0, 1.2, etc
$ docker tag newsnowio/drone-auth-ecr newsnowio/drone-auth-ecr:1.0
$ docker push newsnowio/drone-auth-ecr:1.0
```

### Plugin usage

```
# Make sure drone agent has iam role permission to pull image from ECR
# http://docs.aws.amazon.com/AmazonECR/latest/userguide/RepositoryPolicyExamples.html


# add below lines to .drone.yml

pipeline:
  pull_ecr_images:
    image: newsnow/drone-auth-ecr:1.0
    pull: true
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    commands:
      - docker pull ${accounti_id}.dkr.ecr.${region}.amazonaws.com/${image}

matrix:
  image:
    - application-1
  account_id:
    - 123456789012
  region:
    - us-east-1
```
