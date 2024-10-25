# How to Install ArgoCD on Minikube

* Step:1 Install minikube on remote server
* Step:2 `minikube start`
* Step:3 `kubectl create namespace argocd`
* Step:4 `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
* Step:5 `kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'`
* Step:6 `minikube service argocd-server -n argocd --url` This command will return a URL like http://<minikube-ip>:<node-port>. Save this URL for later.
* Step:7 On your local machine, set up SSH port forwarding to the remote server: `ssh -L 8080:<minikube-ip>:<node-port> user@remote-server-ip`
* Step:8 Open your browser on your personal computer and navigate to: `http://localhost:8080`
* Step:9 Get the initial Argo CD admin password: `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d`
