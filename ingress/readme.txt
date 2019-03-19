https://cert-manager.readthedocs.io/en/latest/tutorials/acme/quick-start/index.html
https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes


kubectl create -f echo1.yaml

kubectl create -f echo2.yaml

kubectl apply -f mandatory.yaml

kubectl apply -f cloud-generic.yaml

kubectl apply -f echo_ingress.yaml


#brew install kubernetes-helm

#helm init

#kubectl create serviceaccount --namespace kube-system tiller

#kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
#kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'

# Install the CustomResourceDefinition resources separately
kubectl apply -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.7/deploy/manifests/00-crds.yaml

# Create the namespace for cert-manager
kubectl create namespace cert-manager

# Label the cert-manager namespace to disable resource validation
kubectl label namespace cert-manager certmanager.k8s.io/disable-validation=true

# Add the Jetstack Helm repository
helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache
helm repo update

# Install the cert-manager Helm chart
helm install \
  --name cert-manager \
  --namespace cert-manager \
  --version v0.7.0 \
  jetstack/cert-manager

kubectl create -f staging_issuer.yaml

kubectl apply -f echo_ingress_ssl.yaml

kubectl describe ingress

kubectl describe certificate

kubectl apply -f echo_ingress_ssl_prod.yaml

kubectl describe ingress

kubectl describe certificate

curl https://echo1.itwnik.com
