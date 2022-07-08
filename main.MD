# get all the pods in default namespace - only pod name without header
kubectl get pods --no-headers | awk '{ print $1 }'

# store the pod list to a file 
kubectl get pods --no-headers | awk '{ print $1 }' > pod_list.txt

# get the node details of all the pods in defult namespace 

cat pod_list.txt | while read lines ; do kubectl describe pods $lines | grep -i node >> node_details.txt ; done
                        
# What does the READY column in the output of the kubectl get pods command indicate?

--> running containers in pod / total containers

1/2 --> means , particular pod has two containers and among 2 one is in active state.

controlplane ~ ➜  kubectl describe pod webapp | grep -i image  --> get the image details for pod

# delete pod : 
controlplane ~ ➜  kubectl delete pod webapp
pod "webapp" deleted

controlplane ~ ➜  kubectl run redis --image=redis123 --dry-run=client -o yaml > redis-pod-defination.yaml

controlplane ~ ➜  vi redis-pod-defination.yaml 

controlplane ~ ➜  kubectl get pods


# you can use ( . ) then kubectl will create all resources from all the manifest yaml file present in current directory
controlplane ~ ➜  kubectl create -f .


pod/redis created



# replace the existing pod with same updated pod. you need to use --force option to delete the existing pod and replace the same pod with updated settings added to the manifest file.
controlplane ~ ➜  kubectl replace -f redis-pod-defination.yaml --force


pod "redis" deleted


pod/redis replaced
