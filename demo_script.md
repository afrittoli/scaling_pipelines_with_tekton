# Demo script

## Tasks

```sh
tkn hub search clone
tkn hub install git-clone
tkn bundle push uk.icr.io/tekton/catalog/demo/deploy-with-ingress:0.1 -f tekton/deploy-task.yaml
```

## Running the pipeline

Provision the pipeline to the cluster:

```sh
kubectl create -f tekton/pipeline.yaml
```

```sh
cat <<EOF > workspace-template.yaml
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
EOF
tkn pipeline start cdcon-demo --workspace name=source,volumeClaimTemplateFile=workspace-template.yaml --workspace name=dockerconfig,secret=regcred
```
