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

