#### Task(s):

 1. Install latest version of mysql helm chart from mybitnami helm repository that you added earlier in your local. Override the rootPassword value of mysql helm chart to something of your choice during installation.
##### Solution:
```
helm install mysql mybitnami/mysql --set="auth.rootPassword=pass@123" --namespace=db --create-namespace
```
 
2. Explore the status of helm release post installation and also the kubernetes resources being created by it
##### Solution:
```
helm status mysql --namespace db

kubectl get all -n db
```
