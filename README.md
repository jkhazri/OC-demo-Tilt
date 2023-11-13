# OneCloud Tilt demo
## what you need to check before preparing your deployment

**Important**: 

Please make sure you have enough resources in your Vcluseter before you start your deployment.

**Best practice :** 
You may need to limit your application ressources by adding what we called ResourceQuota kubernetes kind in your deployment Yaml file.

In this example, I've added a ResourceQuota object that sets resource limits for CPU and memory. Adjust the values based on your application's requirements. You can customize the CPU, memory and ather values according to your application's needs and the available resources in your Kubernetes cluster.

If you need to learn more about the ResourceQuota , please refer to this documentation : https://kubernetes.io/docs/concepts/policy/resource-quotas/

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: php-app-ingress
spec:
  rules:
  - host: docs-vcluster2-443.m1dns.com  # Set the desired domain or hostname here
    http:
      paths:
      - path: /
        pathType: Prefix # type the path that will be used
        backend:
          service:
            name: php-app-clusterip-service
            port:
              number: 20210
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: ingress-resource-quota
spec:
  hard:
    cpu: "500m"  # 0.5 CPU cores
    memory: "512Mi"  # 512 Megabytes of memory

```
# Introduction :
In normal situation dev team write his code and then it push it to the git repo (or any other repo) after that the pipeline is triggered to deploy this code in the K8s cluster as shown in this screen.
![Alt Text](https://github.com/jkhazri/OC-demo-Tilt/blob/main/src/deployment01.png)

Now let suppose the dev team want to test something quickly after changing the code ? ,This mean that they need to go throw the same steps over and over again.

Lets suppose that they have hundreds of changes every day and they don't want to commit them every time to check if the code was well deployed or not ?

Well here come the magic of Tilt. 
Tilt automates all the steps from a code change to a new process: watching files, building container images, and bringing your environment up-to-date. 
Therefore dev team dose not need to push the code every time and the deployment to the k8s cluster is done instantly and the pods are up to date immediately.

![Alt Text](https://github.com/jkhazri/OC-demo-Tilt/blob/main/src/tild-magic.png)

1. Install tilt with:
```bash
curl -fsSL https://raw.githubusercontent.com/tilt-dev/tilt/master/scripts/install.sh | bash
```
2. Run Tilt: Open a terminal in the same directory as your Tiltfile and the PHP project and run the following command:
```bash
git clone https://github.com/jkhazri/OC-demo-Tilt.git
cd OC-demo-Tilt
tilt up
```
3. The tilt file will run the code and deploy the config into the k8s cluster :
```bash
Loading Tiltfile at: OC-demo-Tilt/Tiltfile
Successfully loaded Tiltfile (10.510393ms)
```
4. check the k8s cluster and you will get your pods in return:
```bash
kubectl get deployment

NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
php-app-deployment   3/3     3            3           39m

kubectl get pods

NAME                                  READY   STATUS    RESTARTS   AGE
php-app-deployment-58774855c8-gbfk4   1/1     Running   0          7m30s
php-app-deployment-58774855c8-mgx85   1/1     Running   0          7m30s
php-app-deployment-58774855c8-r7lhw   1/1     Running   0          7m30s

kubectl get ingress

NAME                 CLASS   HOSTS                          ADDRESS           PORTS   AGE
php-app-ingress      nginx   docs-vcluster2.***.com   185.**.**.**3   80      43h

```
   

