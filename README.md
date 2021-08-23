# kubernetes-simple-web
Kubernetes yaml configurations for deployment of the yeasy/simple-web container

# Contents
> simple_web_deploy.yaml --> yaml configuration to deploy yeasy/simple-web docker container. 
>
> The configuration requests for 200MB memory and 0.25 CPU
>
> Port 80 is exposed as port 80 for curl access
>
> A kubernetes service 'simple-web-service' is also defined here

> create_namespace.yaml --> namespace definition for 'devops' namespace