# k8-databases
cicd only works for web tir and app tier launching the databases for through helm charts



Admin

1.Install EBS CSI Drivers.

`````
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.25"
``````

2.provide access to EC2 servers
3.create sc for EBS dynamic provisioning

`````````
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-sc
provisioner: ebs.csi.aws.com
volumeBindingMode: WaitForFirstConsumer
parameters:
  csi.storage.k8s.io/fstype: xfs
  type: io1
  iopsPerGB: "50"
  encrypted: "true"
