Task(s):
 1. In the sample helm chart that you created earlier, add a template that creates ConfigMap shown below Make sure you generate the name for this configmap using helm release name with format : <HELM_RELEASE_NAME>-nginx-configmap

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

2. Also, mount this configmap's index.html content to the pods in Deployment (deployment.yaml template) at location /usr/share/nginx/html/index.html

3. Generate the templates using helm template <path to the sample helm chart> and verify that the changes which you made above are visible

4. Install this helm chart and verify deployment has configmap mounted as needed# Helm Workshop Tasks and Assignment
