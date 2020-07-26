# Steps to provision EKS Cluster in a Jump Box
## Jumpbox configuration

### Before running any commands start GNU screen session
```
screen
```

### Useful screen command
```
screen -ls # lists sessions
screen -x <session number> # connects to your previous session 
```
### Configure account
```
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
```

### Test the variables
```
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

### Configure your acccount on the jumpbox
```
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

### Generate and Import Key Pair
```
ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa

aws ec2 import-key-pair --key-name "eksworkshop" --public-key-material file://~/.ssh/id_rsa.pub

aws kms create-alias --alias-name alias/eksworkshop --target-key-id $(aws kms create-key --query KeyMetadata.Arn --output text)

export MASTER_ARN=$(aws kms describe-key --key-id alias/eksworkshop --query KeyMetadata.Arn --output text)

echo "export MASTER_ARN=${MASTER_ARN}" | tee -a ~/.bash_profile
```

### Enable bash completion
```
eksctl completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```

### Create Cluster yaml
```
cat << EOF > eksworkshop.yaml
---
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: eksworkshop-eksctl
  region: ${AWS_REGION}

managedNodeGroups:
- name: nodegroup
  desiredCapacity: 
  iam:
    withAddonPolicies:
      albIngress: true
secretsEncryption:
  keyARN: ${MASTER_ARN}
EOF
```

### Launch the cluster.  This will take ~15 min.
```
eksctl create cluster -f eksworkshop.yaml
```

### Update kubectl configuration
```
aws eks --region us-east-1 update-kubeconfig --name eksworkshop-eksctl
```

### Test kubectl
```
kubectl get nodes # if we see our 2 nodes, we know we have authenticated correctly
```


