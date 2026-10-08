# demo-frontend

Node.js website linked to a catalog backend API

Catalog: **Component** (website) `demo-frontend` **consumesApis** `demo-backend-api` and **dependsOn** `component:default/demo-backend` in system `acme-demo`.

| Piece | Path |
|---|---|
| App | `server.js` (`GET /health`, page calls backend `/api`) |
| Tests | `npm test` / `npm run lint` |
| Sonar | `sonar-project.properties` |
| CI | `Jenkinsfile` |
| Deploy | `chart/` (Helm + OSSM: Route → Gateway → HTTPRoute, deny-all, STRICT mTLS) |
| IDE | `devfile.yaml` |

```bash
BACKEND_URL=http://demo-backend.demo-dev.svc:8080 npm start
npm run lint
npm test
helm lint chart
```
