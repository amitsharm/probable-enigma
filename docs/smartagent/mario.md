### Create a Namespace called mario

Now that we have eyes on the cluster, let's have some fun!
Namespaces are a way to divide cluster resources between multiple users, teams, projects or applications.
```
kubectl create ns mario
```

### Deploy Super Mario pod 

Deploy a Kubernetes [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/){: target=_blank} named mario and a [Service](https://kubernetes.io/docs/concepts/services-networking/service/){: target=_blank} called mario-external

=== "Shell Command"
    ```text
        kubectl -n mario apply -f mario.yaml 
    ```
=== "Output"
    ```text
        deployment.apps/mario created
        service/mario-external created
    ```
---

You can access your mario pod service by accessing via the load balancer. It takes a few minutes to create Elastic Load Balancers and hooking up networking.

=== "Shell Command"
    ```
        kubectl -n mario get svc
    ```
=== "Output"
    ```text
        NAME             TYPE           CLUSTER-IP     EXTERNAL-IP                                                              PORT(S)        AGE
        mario-external   LoadBalancer   10.100.68.49   aa573ed93a4b645d686ea9a8af5f9eb2-348616612.us-west-2.elb.amazonaws.com   80:31157/TCP   25s
    ```
---    
Copy the EXTERNAL-IP from the output of the above acommand. Point your browser at http://{==EXTERNAL-IP==} and take a few minutes to enjoy the fruits of your labour!

![Super Mario!](https://media.giphy.com/media/l1KtXmfi3EnjM5zpK/giphy.gif)
