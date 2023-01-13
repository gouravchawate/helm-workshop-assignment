#### Task(s):
 1. In the sample helm chart that you created earlier, add a template that creates ConfigMap shown below Make sure you generate the name for this configmap using helm release name with format : <HELM_RELEASE_NAME>-nginx-configmap
```
apiVersion: v1
data:
  index.html: |
    <!DOCTYPE html>
    <html>
    <head>
    <title>Helm Module</title>
    <style>
    html { color-scheme:light dark; }
    body { width: 35em; margin: 0 auto; font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>Helm Module</h1>
    </body>
    </html>
kind: ConfigMap
metadata:
  name: <GENERATE NAME USING HELM RELEASE NAME>
```
##### Solution:
```
apiVersion: v1
data:
  index.html: |
    <!DOCTYPE html>
    <html>
    <head>
    <title>Helm Module</title>
    <style>
    html { color-scheme:light dark; }
    body { width: 35em; margin: 0 auto; font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>Helm Module</h1>
    </body>
    </html>
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-nginx-configmap

```

2. Also, mount this configmap's index.html content to the pods in Deployment (deployment.yaml template) at location /usr/share/nginx/html/index.html
##### Solution:
```
spec:
      volumes:
      - name: configmap-data
        configMap: 
          name: {{ .Release.Name }}-nginx-configmap

containers:
        - name: {{ .Chart.Name }}
          securityContext:
            {{- toYaml .Values.securityContext | nindent 12 }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          volumeMounts:
          - mountPath: /usr/share/nginx/html/index.html
            subPath: index.html
            name: configmap-data

```


3. Generate the templates using helm template <path to the sample helm chart> and verify that the changes which you made above are visible
##### Solution: 
```
helm template mychart

```
4. Install this helm chart and verify deployment has configmap mounted as needed# Helm Workshop Tasks and Assignment
##### Solution:
```
helm install webapp mychart -n webnamespace
```
