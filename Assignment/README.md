
## Assignment

In this module, we have placed few manifests files which needs to be converted to helm templates

Tasks to be achieved :

- [ ] Each and every manifest should be templated such that the name of each kubernetes resource should get generated as `<release_name>-helm-module`. 

  > Tip: Try out defining it at a single place using [named templates](https://helm.sh/docs/chart_template_guide/named_templates/) and reuse it everywhere

- [ ] The [kubernetes service resource](./mychart/templates/nginx-service.yaml) should obtain the value for type of service and port from `values.yaml`

- [ ] The [kubernetes serviceaccount resource](./mychart/templates/nginx-sa.yaml) should be created *conditionally* based on a flag in `values.yaml`. 

  *IF* the flag is true, 

  - serviceaccount will be created using [kubernetes manifest](./mychart/templates/nginx-sa.yaml) provided and [kubernetes deployment resource](./mychart/templates/nginx-deployment.yaml) will be created in this service account

    *ELSE*

  - the serviceaccount creation will be skipped and [kubernetes deployment resource](./mychart/templates/nginx-deployment.yaml) will be created in the `default` serviceaccount

