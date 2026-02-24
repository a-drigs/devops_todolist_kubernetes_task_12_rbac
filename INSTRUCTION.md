kind create cluster --config cluster.yml

bash bootstrap.sh

kubectl get pods -n todoapp
# copy 1 of 2 pods name

kubectl exec -it <copied-pods-name>  -n todoapp -- sh
# go in container

# RUN commands in container to get secrets
TOKEN=$(cat ${SERVICEACCOUNT}/token)
curl --cacert /var/run/secrets/kubernetes.io/serviceaccount/ca.crt -H "Authorization: Bearer $TOKEN" https://kubernetes.default.svc/api/v1/namespaces/todoapp/secrets
