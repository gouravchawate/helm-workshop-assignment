#### Task(s):
 Follow this guide and create a subchart in your existing helm chart from scratch
 Add a bitnami mysql helm chart as the subchart for the existing sample chart you created earlier. Make sure you pass a custom value forrootPassword from your helm chart to mysql helm chart. Install your helm chart and verify the creation of mysql helm chart resources too
 Add a condition in your sample helm chart based on which mysql subchart installation can be enabled / disabled accordingly

##### Solution:
 - Open Chart.yaml and add mysql subchart under dependencies & also define a condition for installing mysql chart as below:
```
dependencies:
- name: mysql
  version: "9.4.6"
  repository: "https://charts.bitnami.com/bitnami"
  condition: mysql.enabled
```
 - Open values.yaml file, pass enabled value and pass a custom Value of rootPassword to mysql helm chart as below:
```
mysql:
 enabled: true
 auth:
  rootPassword: admin
```
 - Installing helm chart and verifying creation of mysql helm chart:
```
helm dependency update mychart

helm install myapp mychart

helm list

kubectl get pods
```


