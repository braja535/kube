Kubernetes Setup and exploring things:


Dashboard Setup :

--> install pods, service accounts using below commands

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml

vagrant@k8s-master:~$ cat admin-user.yml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard

vagrant@k8s-master:~$ cat admin-cluster-role-binding.yml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
---------------------------------------------------------------------------------------------
kubectl apply -f admin-user.yml
kubectl apply -f admin-cluster-role-binding.yml 
kubectl -n kubernetes-dashboard create token admin-user

----------------------------------------------------------------------------------------------

and copy ~/.kube/config file to host machine to ~/.kube/config
then run below commands on host machine.
kubectl proxy --address='0.0.0.0' --port=8001 --accept-hosts='.*'


