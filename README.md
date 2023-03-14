# OpenShift Container Platform Arcade: OCPArcade

Containerize and run retro games in [OpenShift](https://www.openshift.com) and play them in your browser.

## Build and Deploy image in OpenShift

In this example we'll build an image in OpenShift, create service and expose it to the outside world via a route.

```bash
git clone https://github.com/nickschuetz/ocparcade
cd ocparcade/arkanoid
oc new-project ocparcade
oc new-app --strategy=docker --binary --name=arkanoid
oc start-build arkanoid --from-dir .
oc logs deployment/arkanoid -f
oc expose deployment/arkanoid --port 8080
oc expose service/arkanoid
echo http://$(oc get routes arkanoid -n ocparcade -o=jsonpath='{range .spec}{.host}{"\n"}{end}')
```

## Deploy from pre-built image

Here's an example of deploying Epic Pinball from a pre-built image built using Podman and stored in Quay.io

```bash
oc new-project ocparcade
oc new-app quay.io/ocparcade/epicpinball
oc expose service/epicpinball
echo http://$(oc get routes epicpinball -n ocparcade -o=jsonpath='{range .spec}{.host}{"\n"}{end}')
```

## Supporting Open Source Projects

A big thank you to the open source projects that made this possible.

[OpenShift](https://github.com/openshift/)

[Podman](https://podman.io/)

[Quay](https://www.projectquay.io/)

[Universal Base Images](https://access.redhat.com/articles/4238681)

[DOSBox](https://www.dosbox.com/)

[js-dos](https://js-dos.com/)
