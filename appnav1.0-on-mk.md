Install Application Navigator on minikube
  
### Prereqs
1. cloudctl, docker, helm

### Install

1. prereq actions:
   1. set kubectl context
      1. if not already started:
         ```
         minikube start
         ```
      1. if already started:
         ```
         kubectl config use-context minikube
         ```
1. Install appnav chart:
   1. Download or clone the charts from Github.com
          https://github.com/IBM/charts
   1. Install chart
   ```
   helm install --name=app-nav --set env.kubeEnv=minikube <charts location i.e. /charts/stable/ibm-app-navigator> --set appNavUI.service.type=NodePort
   ```
   1. Make sure all prism pods are running (i.e. prism, prism-controller, prism-was-controller)
   ```
   kubectl get pods
   ```   

### Install sample applications
   ```
   kubectl apply -f samples/crds
   helm install --name=stocktrader samples/stocktraderChart
   helm install --name=bookinfo samples/bookinfoChart
   ```
Notes:
1. prereq actions:
   1. Install helm on minikube

      1. Install the helm client on your laptop
      1. Install tiller (the helm server component) on the cluster
      ```
      kubectl create serviceaccount tiller -n kube-system
      kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller -n kube-system
      helm init --upgrade --service-account tiller
      ```
### Bring up app-nav-ui-service to view sample applications or create new application
   ```
   minikube service ibm-app-nav-ui-service
   ```  
   
### Uninstall Helm Chart

   1. Normal: ```helm delete app-nav --purge --tls```
   2. If stuck: ```helm delete app-nav --purge --tls --no-hooks```

   

   
