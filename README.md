# fis-groovy-openshift

Simple Dockerfile, adding groovy into the RedHat fis java images, so now this image contains:

- jdk8
- maven
- groovy

profit.


  docker build -t welshstew/fis-groovy-openshift .
  
## Building on OSE

```
oc new-project groovy
oc create -f kube/fis-groovy-openshift-template.json -n groovy
oc create -f https://raw.githubusercontent.com/jboss-fuse/application-templates/master/fis-image-streams.json -n openshift
REGISTRY=`oc get svc/docker-registry -n default -o json | jq -r .spec.portalIP`
oc new-app --template=fis-groovy-openshift -p REGISTRY=$REGISTRY,IS_PULL_NAMESPACE=groovy

```

## Running a Groovy Job

[Taken from this BLOG](https://blog.openshift.com/openshift-jobs/)

```
oc create -f fis-groovy-job.yaml
```