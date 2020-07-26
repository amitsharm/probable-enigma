### Create a Deployment simulating a failure

Let's simulate some real-world failures. Here we are creating a sample Deployment imagesample

=== "Shell Command"
    ```text
        kubectl apply -f imagesample.yaml
    ```
=== "OUTPUT"
    ```text
        deployment.apps/imagesample created
    ```
However, there is a twist: although the output message says the Deployment has been created we can see something is not right in Kubernetes Navigator
![Deployment Error](../images/smartagent/imagesample-error.png){: .zoom}

Our pod is continuing to stay in [Pending](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/) state. Why is this happening?
Currently Kubernetes Navigator tells us something is wrong but we don't necessarily get the root cause of this. Wait till we get our logging setup with Splunk Cloud, then we will determine the root cause and fix the underlying issue. 

