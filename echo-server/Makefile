namespace ?= echo

#k -n echo annotate ingress echo-server cert-manager.io/cluster-issuer=letsencrypt

.PHONY: echo
echo:
	kubectl create namespace $(namespace)
	kubectl apply -f deployment.yaml -n $(namespace)
	kubectl apply -f ingress.yaml -n $(namespace)

.PHONY: clean-echo
clean-echo:
	kubectl delete - deployment.yaml -n $(namespace)
	kubectl delete - ingress.yaml -n $(namespace)

.PHONY: logs-nginx
logs-nginx:
	kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx -f


.PHONY: oauth2-proxy
oauth2-proxy:
	helm repo add azure-marketplace https://marketplace.azurecr.io/helm/v1/repo
	helm repo update azure-marketplace
	helm install oauth2-proxy azure-marketplace/oauth2-proxy -n ingress-nginx --create-namespace -f oauth2-values.yaml
	kubectl apply -f oauth2-ingress.yaml -n ingress-nginx
# helm repo add bitnami https://charts.bitnami.com/bitnami
# helm install my-release bitnami/oauth2-proxy

.PHONY: update-oauth2
update-oauth2:
helm upgrade oauth2-proxy azure-marketplace/oauth2-proxy -f oauth2-values.yaml -n ingress-nginx

.PHONY: ingress-nginx
ingress-nginx:
	helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
	helm repo update ingress-nginx
	helm search repo ingress-nginx
	helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace --wait


.PHONY: clean-ingress
clean-ingress:
	-helm --namespace ingress-nginx uninstall ingress-nginx
	-kubectl delete -n ingress-nginx pvc -l app.kubernetes.io/instance=ingress-nginx
	-kubectl delete namespace ingress-nginx

