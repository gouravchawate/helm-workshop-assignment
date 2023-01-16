#### Task(s):
 Create a pre-install and post-delete hook in your existing sample helm chart that simply runs a Kubernetes job with a busybox image and prints the output I am performing prerequisite tasks! and I am done with cleanup! respectively. Make sure you persist the resources created by hook so that you can verify your changes post install & post uninstall of your chart.

##### Solution:

-  Pre-Install Hook:

```
apiVersion: batch/v1
kind: Job
metadata:
  name: pre-install-job
  annotations:
    "helm.sh/hook": pre-install
spec:
  template:
    spec:
      containers:
      - name: pre-install-job
        image: alpine
        command: ["echo",  "I am performing prerequisite tasks!"]
      restartPolicy: Never

```

- Post-Delete Hook:

```
apiVersion: batch/v1
kind: Job
metadata:
  name: post-delete-job
  annotations:
    "helm.sh/hook": post-delete
spec:
  template:
    spec:
      containers:
      - name: post-delete-job
        image: alpine
        command: ["echo",  "I am done with cleanup!"]
      restartPolicy: Never

```
