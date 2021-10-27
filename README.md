# VMware Cloud on AWS with Tanzu services Demos

These files were used in the following [VMware Cloud on AWS with Tanzu services](https://williamlam.com/2021/10/quick-demo-videos-of-new-vmware-cloud-with-tanzu-services.html) demo videos.

## **Demo 1** - Enabling Tanzu services on VMware Cloud on AWS

N/A

## **Demo 2** - Create vSphere Namespace on VMware Cloud on AWS with Tanzu services

N/A

## **Demo 3** - Deploy Tanzu Kubernetes Cluster (TKC) on VMware Cloud on AWS with Tanzu services

Step 1 - Update [tkc.yaml](tkc.yaml) with the correct vSphere Namespace under `namespace` property along with other parameters for your TKC deployment.


Step 2 - To create TKC, run the following command after logging into the Supervisor Cluster

```bash
kubectl apply -f tkc.yaml
```

## **Demo 4** - Deploy demo application (consuming Storage & Networking services) on Tanzu Kubernetes Cluster (TKC) running on VMware Cloud on AWS with Tanzu services

**Note:** For more details about this demo (Thanks to Ivan Font) and many others, please refer to this blog post [Interesting Kubernetes application demos](https://williamlam.com/2020/06/interesting-kubernetes-application-demos.html)

Step 1 - Disable default Pod Security Policies (PSP) before deploying the example application

Step 2 - Create Kubernetes `demo` namespace:

```bash
kubectl create ns demo
```

Step 2 - Create Mongo DB PVC

```bash
kubectl apply -f mongo-pvc.yaml
```

Verify PVC was successfully created and bounded by running:

```bash
kubectl -n demo get pvc
```

Step 3 - Create Mongo DB deployment

```bash
kubectl apply -f demo-deployment.yaml
```

Verify PVC was successfully created and bounded by running:

```bash
kubectl -n demo get deploy/mongo
```

Step 4 - Create Demo application deployment

```bash
kubectl apply -f demo-deployment.yaml
```

Verify PVC was successfully created and bounded by running:

```bash
kubectl -n demo get deploy/mongo
```

Step 5 - Create Demo service (type LoadBalancer)

```bash
kubectl apply -f demo-service.yaml
```

Verify Load Balancer was successfully created by running:

```bash
kubectl -n demo get svc
```

## **Demo 5** - Using Tanzu Mission Control (TMC) to deploy Tanzu Kubernetes Cluster (TKC) running on VMware Cloud on AWS with Tanzu

Step 1 - You will need to register your Supervisor Cluster with [Tanzu Mission Control service](https://tanzu.vmware.com/mission-control). Retrieve the registration URL and update [register_in_tmc.yaml](register_in_tmc.yaml) the `registrationLink` property. You may also need to update the `namespace` depending on id that was created within your Supervisor Cluster. You can check by running `kubectl get ns | grep tmc`

Step 2 - Register your Supervisor Cluster with Tanzu Mission Control by running:

```bash
kubectl apply -f register_in_tmc.yaml
```

## **Demo 6** - Deploy Virtual Machines using VMware Cloud on AWS with Tanzu services

Step 1 - Update [centos.yaml](centos.yaml) with your desired configuration including guest configurations such as passwords and SSH keys

Step 2 - To create Virtual Machine using the VM Service, run the following command:

```bash
kubectl apply -f centos.yaml
```

Verify VM was successfully created by running:

```bash
kubectl get vm
```