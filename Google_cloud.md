## Mac [sdk_click_here](https://cloud.google.com/sdk/docs/install#mac)
## windows gcld_sdk
```
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")

& $env:Temp\GoogleCloudSDKInstaller.exe
```    
## configure:
```
gcloud init
```


## GKE cluster 

```
gcloud container clusters create hello-cluster --num-nodes=1
```

## To get cluster congfig:
```
gcloud container clusters get-credentials hello-cluster
```
## create service & delete it 

```
kubectl create deployment hello-server \
    --image=us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

```
kubectl expose deployment hello-server --type LoadBalancer --port 80 --target-port 8080
```

```
kubectl get pods
kubectl get service hello-server
```

# Delete service & cluster 
```
kubectl delete service hello-server
gcloud container clusters delete hello-cluster
```
