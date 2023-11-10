# onecloud Tilt demo
Intro :
In normal situation dev team write his code and then it push it to the git repo (or any other repo) after that the pipeline is triggered to deploy this code in the K8s cluster as shown in this screen.
![Alt Text](https://github.com/jkhazri/OC-demo-Tilt/blob/main/src/deployment01.png)

Now let suppose the dev team want to test something quickly after changing the code ? ,This mean that they need to go throw the same steps over and over again.

Lets suppose that they have hundreds of changes every day and they don't want to commit them every time to check if the code was well deployed or not ?

Well here come the magic of Tilt. 
Tilt automates all the steps from a code change to a new process: watching files, building container images, and bringing your environment up-to-date. 
Therefore dev team dose not need to push the code every time and the deployment to the k8s cluster is done instantly and the pods are up to date immediately.

![Alt Text](https://github.com/jkhazri/OC-demo-Tilt/blob/main/src/tild-magic.png)

1. Install tilt with:
```
curl -fsSL https://raw.githubusercontent.com/tilt-dev/tilt/master/scripts/install.sh | bash
```
2. Run Tilt: Open a terminal in the same directory as your Tiltfile and the PHP project and run the following command:
```
git clone https://github.com/jkhazri/OC-demo-Tilt.git
cd OC-demo-Tilt
tilt up
```
3. The tilt file will run the code and deploy the config into the k8s cluster :
```
Loading Tiltfile at: OC-demo-Tilt/Tiltfile
Successfully loaded Tiltfile (10.510393ms)
```
4. check the k8s cluster and you will get your pods in return:
```
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
   

