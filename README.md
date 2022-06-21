# GitOps-managed OpenShift ServiceMesh

This guide details the implementation and configuration steps to setup OpenShift Service Mesh (OSSM) v2.1, including Control Plane and dependent components and operators.

Do not use the `base` directory directly, as you will need to patch the `channel` based on the version of OpenShift you are using, or the version of the operator you want to use.

## Provision Service Mesh with the CLI

TIP: Commands shown are show from the root of a clone of this Git repository.

Install the OpenShift Elasticsearch operator

```
oc apply -k elasticsearch-operator/overlays/stable
```

Install the OpenShift Distributed Tracing operator

```
oc apply -k openshift-distributed-tracing-operator/overlays/stable
```

Install the Kiali operator

```
oc apply -k kiali-operator/overlays/stable
```

Install OpenShift Service Mesh

```
oc apply -k openshift-servicemesh/operator/overlays/stable
```

Configure the service mesh control plane

```
oc apply -k openshift-servicemesh/instance/overlays/default
```

## Provision Service Mesh with ArgoCD

TBD...
