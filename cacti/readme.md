This code is just an example and has been written to be run in production

## Prerequisites
1. You need to run your script to configure the EKS cluster with the Service 
account and the correct permissions to this
2. Using your information about your cluster modify the environment variables shown below
3. Using your cluster and environment information modify the variables in the ./helm/values.yaml file

follow the steps bellow to test your cluster

## Deploying your product to test the EKS cluster configuration

* This commands are to be run in a terminal with access to your AWS account.
* You need the aws cli and kubectl installed 

**Modify this variables with the correct values for your product** 

```
export PRODUCT_NAME=example
export AWS_REGION=us-east-1
export PRODUCT_VERSION=v1
export PRODUCT_CODE=1jvwme1n9wao4epdu6hi9y1rr
export ECR_REPOSITORY=453854455992.dkr.ecr.us-east-1.amazonaws.com/eks
```

**To build the image and tagging it to be pushed**

```
docker build -t ${ECR_REPOSITORY}:${PRODUCT_VERSION} .
aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REPOSITORY}:${PRODUCT_VERSION}
```

**Pushing the imate to the ECR Repository**

```
docker push ${ECR_REPOSITORY}:${PRODUCT_VERSION}
```

**Deploying the product to the cluster**

```
helm install ${PRODUCT_NAME} ./helm
```

**To check that the pod is running**
```
kubectl get pods
```


**To read the logs of the pod and see if the call was successfull**
```
kubectl logs <Pod Name>
```

**To update to a new version the product**

```
helm upgrade ${PRODUCT_NAME} ./helm
```

**To uninstall the product**

```
helm uninstall ${PRODUCT_NAME}
```
    

**Quick redeploy**
```
docker build -t ${ECR_REPOSITORY}:${PRODUCT_VERSION} .
aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REPOSITORY}:${PRODUCT_VERSION}
docker push ${ECR_REPOSITORY}:${PRODUCT_VERSION}
helm upgrade ${PRODUCT_NAME} ./helm
kubectl get pods
kubectl logs -f  
```




