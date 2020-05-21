# Anthos Configuration Management Directory

This is the root directory for Anthos Configuration Management.

See [our documentation](https://cloud.google.com/anthos-config-management/docs/repo) for how to use each subdirectory.

Anthos-config-managememnt syncs with the foo-corp Directory (this can be set to whatever name you like)

Security templates not in use on the cluster are found in the void folder.

# To install ACM:

## Deploy operator:

https://cloud.google.com/anthos-config-management/docs/how-to/installing#deploying

## Setup git credentials: (ACM is read only so you can use none)

https://cloud.google.com/anthos-config-management/docs/how-to/installing#git-creds-secret

## Configure the operator:

# config-management.yaml

# apiVersion: configmanagement.gke.io/v1
# kind: ConfigManagement
# metadata:
#   name: config-management
# spec:
# clusterName is required and must be unique among all managed clusters
#   clusterName: user1
#This will install Gatekeeper policy controller (not sure if its full features)
#   policyController:
#     enabled: true
#   git:
#     syncRepo: https://github.com/davidmitchell2019/anthos-config-management.git
#     syncBranch: master
#     secretType: none
# which directory to sync with ACM  
#     policyDir: "foo-corp"

## Gatekeeper can also be deployed

kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml
kubectl get crd | grep -i constraint
kubectl get constrainttemplates

## Check config management deployment

kubectl -n kube-system get pods | grep config-management

## Get the logs for the config management operator: (useful for troubleshooting syncs)

kubectl -n kube-system logs -l k8s-app=config-management-operator

## Install nomos

gsutil cp gs://config-management-release/released/latest/linux_amd64/nomos nomos
chmod 400 nomos && mv nomos /usr/local/bin

## Check the status of your sync: (useful for troubleshooting syncs)

nomos status
