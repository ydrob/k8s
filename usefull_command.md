
kubectl -n kubernetes-dashboard port-forward svc/kubernetes-dashboard  8001:443


kubectl patch svc ingress-nginx-controller -n ingress-nginx -p '{"spec": {"type": "LoadBalancer", "externalIPs":["172.21.0.6"]}}'
