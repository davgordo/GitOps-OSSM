# GitOps-managed OpenShift ServiceMesh

This guide details the implementation and configuration steps to setup OpenShift Service Mesh (OSSM) v2.1, including Control Plane and dependent components and operators.

Do not use the `base` directory directly, as you will need to patch the `channel` based on the version of OpenShift you are using, or the version of the operator you want to use.

## Provision OpenShift Service Mesh with the OpenShift CLI

TIP: Commands are shown from the root of a clone of this Git repository.

Install the OpenShift Elasticsearch operator:

```
oc apply -k elasticsearch-operator/overlays/stable
```

Install the OpenShift Distributed Tracing operator:

```
oc apply -k openshift-distributed-tracing-operator/overlays/stable
```

Install the Kiali operator:

```
oc apply -k kiali-operator/overlays/stable
```

Install OpenShift Service Mesh:

```
oc apply -k openshift-servicemesh/operator/overlays/stable
```

Configure the service mesh control plane:

```
oc apply -k openshift-servicemesh/instance/overlays/default
```

## How to use this library

You can remotely target the provided overlays and combine them, for example:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - https://github.com/RHC-STP-OSSM/GitOps-OSSM/elasticsearch-operator/overlays/stable
  - https://github.com/RHC-STP-OSSM/GitOps-OSSM/openshift-distributed-tracing-operator/overlays/stable
  - https://github.com/RHC-STP-OSSM/GitOps-OSSM/kiali-operator/overlays/stable
  - https://github.com/RHC-STP-OSSM/GitOps-OSSM/openshift-servicemesh/operator/overlays/stable
  - https://github.com/RHC-STP-OSSM/GitOps-OSSM/openshift-servicemesh/instance/overlays/default
```

You may also want to supplement, overwrite, or merge your own configuration along with the artifacts from this library. An [example repository](https://github.com/RHC-STP-OSSM/cluster-gitops) is provided that can be used as a starting point for managing a cluster using these core templates. The example repository contains a reference `kustomization` and ArgoCD `Application`.
