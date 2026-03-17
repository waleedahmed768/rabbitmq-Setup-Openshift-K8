# rabbitmq-Setup-Openshift-K8
$kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"
# namespace/rabbitmq-system created
# customresourcedefinition.apiextensions.k8s.io/rabbitmqclusters.rabbitmq.com created
# serviceaccount/rabbitmq-cluster-operator created
# role.rbac.authorization.k8s.io/rabbitmq-cluster-leader-election-role created
# clusterrole.rbac.authorization.k8s.io/rabbitmq-cluster-operator-role created
# rolebinding.rbac.authorization.k8s.io/rabbitmq-cluster-leader-election-rolebinding created
# clusterrolebinding.rbac.authorization.k8s.io/rabbitmq-cluster-operator-rolebinding created
# deployment.apps/rabbitmq-cluster-operator created


$kubectl get all -n rabbitmq-system

NAME                                             READY   STATUS    RESTARTS   AGE
pod/rabbitmq-cluster-operator-54f948d8b6-k79kd   1/1     Running   0          2m10s

NAME                                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/rabbitmq-cluster-operator   1/1     1            1           2m10s

NAME                                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/rabbitmq-cluster-operator-54f948d8b6   1         1         1       2m10s

$kubectl get customresourcedefinitions.apiextensions.k8s.io
NAME                                             CREATED AT
...
rabbitmqclusters.rabbitmq.com                    2021-01-14T11:12:26Z
...
