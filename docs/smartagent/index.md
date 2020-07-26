# Introduction

Now that you have deployed a Kubernetes cluster on [Amazon EKS](https://aws.amazon.com/eks/){: target=_blank}, it's time to set up monitoring and deploy applications.

We will start by deploying SignalFx SmartAgent to our Kubernetes cluster. SignalFx is the real-time cloud monitoring solution acquired by Splunk in October 2019.

The workshop also introduces you to dashboards, editing and creating charts, creating detectors to fire alerts, Monitoring as Code[^3] and the SignalFx Service Bureau[^3] capabilities in SignalFx

<b> A Word About SignalFx Real-time Streaming Architecture </b>

![SFx Architecture](../images/smartagent/signalfx_metrics_architecture.png){: .zoom}

By the end of this technical workshop you will have a good understanding of some of the key features and capabilities of the SignalFx platform.
