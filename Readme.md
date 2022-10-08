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
eyJhbGciOiJSUzI1NiIsImtpZCI6Ik0zeXJMTUs4MzN2SzUxVVQ0YVd2Q2xWLVNkVFBCbGhVc2lkdms5cVVaQm8ifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNjY1MDI5OTkyLCJpYXQiOjE2NjUwMjYzOTIsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsInNlcnZpY2VhY2NvdW50Ijp7Im5hbWUiOiJhZG1pbi11c2VyIiwidWlkIjoiMzhkZjVmYWQtYmZlZS00YTNiLWI3YjQtM2VlN2VlZjY3NGQzIn19LCJuYmYiOjE2NjUwMjYzOTIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlcm5ldGVzLWRhc2hib2FyZDphZG1pbi11c2VyIn0.NYNiEFHiIyKeWq3Z50lsfk3Bw7Br9nbyJgkHsghPbh1abDWYWNeT4Qe3OZpUbYU0wNNT_mjomZT_z0DohiDOIpj1XSIQP3o_IYzG8IE31HrID2afyhfKZVi8uYZ9KrPAW8mQCxMLcuUaZi81m3pHlYO1pHP0XppM7IIT_V8qJWlk4xUAkgo_jVpZPBJmXbUPFGqxphke-oAacaP8HkNX3KNM2Gs8AIM1TCyZGeXpQ6eqiAdFIbo9YRQgoCwHKCKypN_QiN3j1s-8rsIytzVcAiS0k46fQUvj4LW84rPnr1aHp1UUdYDAVqRPiPCdqXbakTlxJ3-3Ta3GIfi8qiXC8w
----------------------------------------------------------------------------------------------

and copy ~/.kube/config file to host machine to ~/.kube/config
then run below commands on host machine.
kubectl proxy --address='0.0.0.0' --port=8001 --accept-hosts='.*'


