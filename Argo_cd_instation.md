# Install Argo CD

## Step 1:

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### If you are not interested in UI, SSO, multi-cluster features then you can install core Argo CD components only:
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
```

## Step 2: Install Argo CD Cli 

* mac 
```
brew install argocd
```
* windows & linux [clickhere](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

## step 3: Access The Argo CD API Server
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
## step 4: ingress argo cd 
### [Refer document for configuration](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/)

## Port Forwarding
## Kubectl port-forwarding can also be used to connect to the API server without exposing the service.
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
### Note : The API server can then be accessed using the localhost:8080

## step 5:  Login Using The CLI
### The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. You can simply retrieve this password using kubectl:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
### Note: You should delete the argocd-initial-admin-secret from the Argo CD namespace once you changed the password. The secret serves no other purpose than to store the initially generated password in clear and can safely be deleted at any time. It will be re-created on demand by Argo CD if a new admin password must be re-generated.

## Using the username admin and the password from above, login to Argo CD's IP or hostname:
```
argocd login <ARGOCD_SERVER>
```
### Note: ```The CLI environment must be able to communicate with the Argo CD controller. If it isn't directly accessible as described above in step 3, you can tell the CLI to access it using port forwarding through one of these mechanisms: 1) add --port-forward-namespace argocd flag to every CLI command; or 2) set ARGOCD_OPTS environment variable: export ARGOCD_OPTS='--port-forward-namespace argocd'.```

## Register A Cluster To Deploy Apps To (Optional):

### First list all clusters contexts in your current kubeconfig:
```
kubectl config get-contexts -o name
```
### Creating Apps Via CLI 
* Create the example guestbook application with the following command:
```
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default`

```
