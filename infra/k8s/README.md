# Option 1 Kubernetes Manifests

Apply order:

```bash
kubectl apply -f namespace.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.example.yaml
kubectl apply -f milvus-alias-service.yaml
kubectl apply -f translator.yaml
kubectl apply -f agent.yaml
kubectl apply -f frontend.yaml
```

Before applying:

1. Replace all image placeholders:
   - `REGION-docker.pkg.dev/PROJECT_ID/REPO_NAME/translator:latest`
   - `REGION-docker.pkg.dev/PROJECT_ID/REPO_NAME/agent:latest`
   - `REGION-docker.pkg.dev/PROJECT_ID/REPO_NAME/frontend:latest`
2. Replace `GOOGLE_API_KEY` in `secret.example.yaml`.
3. If Milvus namespace/service name differs, update `milvus-alias-service.yaml` and/or `MILVUS_HOST` in `configmap.yaml`.

This setup includes:

- Internal ClusterIP services for Translator and Agent
- LoadBalancer service for Streamlit frontend
- HPA for Translator and Agent with CPU >= 70%, min 1 max 5

