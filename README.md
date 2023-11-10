# onecloud Tilt demo
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
kubectl get pods

NAME                                  READY   STATUS    RESTARTS   AGE
php-app-deployment-58774855c8-gbfk4   1/1     Running   0          7m30s
php-app-deployment-58774855c8-mgx85   1/1     Running   0          7m30s
php-app-deployment-58774855c8-r7lhw   1/1     Running   0          7m30s

kubectl get svc

NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes                  ClusterIP   10.99.253.6      <none>        443/TCP          3d23h
php-app-clusterip-service   ClusterIP   10.108.58.62     <none>        20210/TCP        43h

```
   

