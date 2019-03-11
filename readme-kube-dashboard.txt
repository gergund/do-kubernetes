
Get YAML manifest:
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml

Get token: 
#kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t'

Run proxy:
#kubectl proxy

HTTP browser access: 
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
