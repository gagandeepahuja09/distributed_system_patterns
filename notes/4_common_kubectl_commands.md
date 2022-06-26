**Namespaces**
* k8s uses namespaces to organize objects in a cluster.
* We can think of each namespace as a folder that holds a set of objects.
* If we want to interact with all namespace - for example to list all pods in our cluster, we can pass the --all-namespaces flag.

**Contexts**
* If we want to set the default namespace more permanently, we can use context.
* This gets recorded in a kubectl config file: $HOME/.kube/config.
* This config file also stores how to both find and authenticate our cluster.
* Better use: With the set-context command, we can manage different clusters or different users for authenticating to those clusters using the --users or --clusters.
* **kubectl config set-cluster dev-cluster**
* **kubectl config set-context dev-cluster --cluster dev-cluster --user=gagandeepahuja09@gmail.com**
* **kubectl use-context dev-cluster**