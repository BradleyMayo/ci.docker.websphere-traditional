### Example setup for using OpenShift Pipelines to build and deploy the hello-world sample

## Create a new project
oc new-project hello-world-pipeline

## If the openshift-pipelines-operator isn't installed subscribe to it
oc apply -f pipeline/subscription.yaml

## Install tasks
oc create -f pipeline/update_deployment_task.yaml
oc create -f pipeline/apply_manifest_task.yaml

## Install pipeline
oc create -f pipeline/pipeline.yaml

## Install pipeline resources
oc create -f pipeline/resources.yaml

## A limitation was removed in the tektoncd buildah support
oc apply -f pipeline/buildah.yaml

## Start the pipeline
tkn pipeline start build-and-deploy
