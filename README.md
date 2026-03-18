# rabbitmq-Setup-Openshift-K8
https://github.com/rabbitmq/cluster-operator/blob/main/docs/examples/additionalPorts/rabbitmq.yaml

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
$oc adm policy add-scc-to-user privileged -z rabbitmq-server -n rabbitmq-system
$kubectl apply -f rabbitmq.yaml

$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                                             READY   STATUS    RESTARTS   AGE
pod/rabbitmq-cluster-operator-69bdbd88b7-t42dk   1/1     Running   0          37m
pod/rabbitmq-server-0                            1/1     Running   0          33m

NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                        AGE
service/rabbitmq         ClusterIP   172.30.81.196   <none>        5672/TCP,15672/TCP,15692/TCP   33m
service/rabbitmq-nodes   ClusterIP   None            <none>        4369/TCP,25672/TCP             33m

NAME                                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/rabbitmq-cluster-operator   1/1     1            1           37m

NAME                                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/rabbitmq-cluster-operator-69bdbd88b7   1         1         1       37m

NAME                               READY   AGE
statefulset.apps/rabbitmq-server   1/1     33m

NAME                                              IMAGE REPOSITORY                                                                                    TAGS               UPDATED
imagestream.image.openshift.io/rabbitmq           default-route-openshift-image-registry.apps.test.com.pk/rabbitmq-system/rabbitmq           4.1.3-management   35 minutes ago
imagestream.image.openshift.io/rabbitmqoperator   default-route-openshift-image-registry.apps.test.com.pk/rabbitmq-system/rabbitmqoperator   2.19.2             37 minutes ago

NAME                                                HOST/PORT                  PATH   SERVICES   PORT         TERMINATION   WILDCARD
route.route.openshift.io/dev-rabbitmq.test.com.pk   dev-rabbitmq.test.com.pk   /      rabbitmq   management                 None

NAME                                    ALLREPLICASREADY   RECONCILESUCCESS   AGE
rabbitmqcluster.rabbitmq.com/rabbitmq   True               True               33m

