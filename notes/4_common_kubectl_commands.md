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
* **kubectl config set-context dev-ctx --cluster dev-cluster --user=gagandeepahuja09@gmail.com**
* **kubectl use-context dev-ctx**

**Viewing Kubernetes API Objects**
* Everything contained in Kubernetes is represent by a RESTful resource. These resources are referred as k8s objects.
* The kubectl command makes HTTP requests to URLs to access the k8 object residing at that path.
* A listing of all the resources in the current namespace: **kubectl get [resource-name]**
* Get a specific resource: **kubectl get [resource-name] [obj-name]**
* -o wide flag to get slightly more details. -o json or -o yaml flags for viewing the object as json or yaml.
* --no-headers flag to remove the header from the output table. We can manipulate the output using unix pipes. (kubectl ... | awk ..)
* Extracting specific fields from the object using JSONPath query language.
    **kubectl get pods my-pod -o jsonpath --template={.status.podIP}**
* For more details of a particular 