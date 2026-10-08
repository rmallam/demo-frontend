# demo-frontend

Node.js website linked to a catalog backend API

Website for system **acme-demo**. Depends on `component:default/demo-backend` and consumes `api:default/demo-backend-api`. In-cluster it calls `http://demo-backend.demo-dev.svc:8080/api`.

## Pipeline

Jenkinsfile stages: **Install → Lint → Unit tests → SonarQube → Helm lint**.

Point a Jenkins job named `demo/demo-frontend` at this repo. Set credential `SONAR_TOKEN` to run the scanner against `http://sonarqube.sonarqube.svc:9000`.

## Deploy

North-south is **OpenShift Route → Gateway API Gateway → HTTPRoute → app**. AuthZ in this chart is **deny-all** plus ALLOW from the ingress gateway. **STRICT mTLS** is namespace-wide (Kyverno on enroll).

```bash
oc label namespace demo-dev acme.io/mesh-enroll=true istio.io/dataplane-mode=ambient --overwrite
helm upgrade --install demo-frontend chart -n demo-dev
```

Ingress: `https://demo-frontend-demo-dev.apps.rosa.rosa-89s85.bhg0.p3.openshiftapps.com`

The chart labels pods `backstage.io/kubernetes-id=demo-frontend` for Topology.

## Dev Spaces

https://devspaces.apps.rosa.rosa-89s85.bhg0.p3.openshiftapps.com#https://github.com/rmallam/demo-frontend?new&devfilePath=devfile.yaml
