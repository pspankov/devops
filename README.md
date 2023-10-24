# Notes

## kubectl
```bash
kubectl get deployments -n <namespace>
kubectl get pods -n <namespace>
kubectl delete pod <pod-name> -n <namespace>
kubectl describe pod <pod-name> - n <namespace>
kubectl get pods -n <namespace> -o wide
kubectl exec -it <pod-name> -n <namespace> -- /bin/sh
kubectl logs -f <pod-name> -n <namespace>
kubectl get services -n <namespace>
kubectl get svc -n <namespace>




kubectl get po --all-namespaces
k0s kubectl get po --all-namespaces

k0sctl apply --config k0s.yaml

k0s kubectl create namespace flux-system

kubectl get po -n rabbitmq

kubectl get svc -n rabbitmq

# for testing
kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml
kubectl exec -ti dnsutils -- bash
nslookup shared-rabbitmq

# run busybox in interactive mode
kubectl run -i --tty busybox --image=busybox --restart=Never -- sh

# curl deploy
kubectl run mycurlpod --image=curlimages/curl -i --tty -- sh

kubectl get secret -n rabbitmq
kubectl get secret -n rabbitmq shared-rabbitmq-default-user -oyaml
echo 'base64string' | base64 -d

export GIT_PASSWORD=

kubectl port-forward -n rabbitmq svc/shared-rabbitmq 15672:15672

k0s kubectl get secret -n flux-system

gpg --import sops.pub.asc

kubectl get secret -n minio minio-creds -oyaml
kubectl get svc -n minio minio-creds -oyaml
kubectl get po -n minio
kubectl logs -f -n minio minio-deployment-66b44cd6bd-np7m8

kubectl get secret -n dev
kubectl delete secret docerk-creds

sops --encrypt --in-place --config .sops.yml ../fitting/chart/templates/secret/docker-secret.yaml


# create docker-registry secret from values
kubectl create secret docker-registry test-regcred -n dev --docker-server=harbor.harbor.svc.cluster.local --docker-username=your-name --docker-password=your-pword


# create unencrpyted docker secret file
kubectl create secret generic docker-creds --from-file=.dockerconfigjson=/home/pavel/.docker/config.json  --type=kubernetes.io/dockerconfigjson --dry-run=client -o yaml
# create empty configmap
kubectl create configmap api-config --dry-run=client -o yaml

k0sctl reset --config k8s/k0s.yaml
systemctl reboot


# port forwarding
kubectl port-forward -n dev svc/minio 9000:9000

# deploy nginx ingress controller
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.0/deploy/static/provider/cloud/deploy.yaml

# expose deployment/service
kubectl expose deployment harbor-portal --type=NodePort --name=exposed-harbor-registry -n harbor

# disable tls cert check
kubectl config set-cluster sizecatch --insecure-skip-tls-verify=true

```

minio - create bucket manually
```bash
kubectl exec -it minio-deployment-d46b5cd8b-spz72 -n dev -- /bin/sh
curl -o /usr/local/bin/mc https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x /usr/local/bin/mc
mc --version
mc config host add sizecatchminio http://minio.dev.svc.cluster.local:9000 minioadmin minioadmin
mc mb --ignore-existing sizecatchminio/s3-static-staging
mc mb --ignore-existing sizecatchminio/
```

## k0s

## flux

```bash
flux reconcile kustomization app --with-source
flux reconcile source git flux-system
flux reconcile source git fitting-git

flux suspend hr fitting -n dev
flux resume hr fitting -n dev
```

## tekton



# git

disable ssl verification
```bash
git config http.sslVerify false
```

## Sources

* https://k0sproject.io/
* https://github.com/k0sproject/k0sctl
* https://fluxcd.io
* https://tekton.dev/
* https://kustomize.io/
