#### Task(s):
 Create a test hook in your sample helm chart which validates that nginx service is up
##### Solution:
- Open mychart/templates/tests/test-connection.yml and update test details
```
apiVersion: v1
kind: Pod
metadata:
  name: "{{ include "mychart.fullname" . }}-test-connection"
  labels:
    {{- include "mychart.labels" . | nindent 4 }}
  annotations:
    "helm.sh/hook": test
spec:
  containers:
    - name: wget
      image: busybox
      command: ['wget']
      args: ['{{ include "mychart.fullname" . }}:{{ .Values.service.port }}']
  restartPolicy: Never
```

- Run below command to test:
```
helm test myrelease
```
