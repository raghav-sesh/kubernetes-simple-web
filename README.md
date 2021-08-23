# kubernetes-simple-web
Kubernetes yaml configurations for deployment of the [yeasy/simple-web](https://hub.docker.com/r/yeasy/simple-web/) container in a GKE cluster

# Contents
> __simple_web_deploy.yaml__ --> yaml configuration to deploy yeasy/simple-web docker container. 
>
> The configuration requests for 100MB memory and 0.1 CPU for each container deployment. Replicas is set to 3, i.e., 3 pods
>
> Port 80 is exposed as port 80 for curl access
>
> A kubernetes service 'simple-web-service' is also defined here

> __create_namespace.yaml__ --> namespace definition for 'devops' namespace

# Prerequisites
1. kubectl and kubectx must be setup on the machine
2. gcloud credentials for kubectl to authenticate into the GKE cluster

# Deploying the container
1. Get the gcloud credentials so that kubectl is able to fetch it from its config

&nbsp;&nbsp;&nbsp;&nbsp;Command: gcloud container clusters get-credentials "cluster-name" --region "region-name"

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 9 51 14 AM](https://user-images.githubusercontent.com/22592043/130486130-488849b0-4deb-47df-903a-51a96704d3d1.png)

2. Run kubectx to confirm context. The context should output the GCP project and the cluster name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 9 52 27 AM](https://user-images.githubusercontent.com/22592043/130486313-788820d8-4dc8-44cd-8e89-63a7a83c228a.png)

3. Create the devops namespace to avoid conflicts with other users

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 9 54 38 AM](https://user-images.githubusercontent.com/22592043/130486570-15e38c0f-3c37-4966-b3ae-1799e5847b02.png)

4. Switch to devops namespace

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 9 56 17 AM](https://user-images.githubusercontent.com/22592043/130486797-075dd93d-1b1c-496e-8826-b051224fb553.png)

5. Deploy pods by running kubectl create with the simple_web_deploy.yaml file

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 9 57 47 AM](https://user-images.githubusercontent.com/22592043/130487027-c8427f09-3bfe-4b3b-baa8-1a901d7dff82.png)

6. Verify that pods are running by getting the pods from devops namespace. Note that it might take a few minutes for the containers to get deployed

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 10 08 25 AM](https://user-images.githubusercontent.com/22592043/130488330-4735e74c-58fc-4b21-8ac9-7e9a9a48b6ce.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can also look at the running pods in the GCP dashboard like this:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Screenshot 2021-08-23 at 10 12 31 AM](https://user-images.githubusercontent.com/22592043/130488896-67604dbb-e209-4fc3-974e-2368a63f08c7.png)

7. An interactive bash session can be launched inside one of the pods by running 'kubectl exec -it ___pod-name___ bash'


# Further...
[Cluster Role Binding](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) to restrict access to the pods based on user authorization
