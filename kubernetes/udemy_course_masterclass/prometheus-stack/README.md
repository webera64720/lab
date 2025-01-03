helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace=monitoring --create-namespace

kubectl --namespace monitoring get pods -l "release=prometheus-stack"

helm show values prometheus-community/kube-prometheus-stack > prometheus-default-values.yaml


Service:
  k describe svc -n monitoring prometheus-stack-grafana | grep Selector                                                                                                                                            Selector:                 app.kubernetes.io/instance=prometheus-stack,app.kubernetes.io/name=grafana
