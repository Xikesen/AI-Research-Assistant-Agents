# Terraform script to deploy Milvus into an existing GKE cluster

This folder now reuses an already-created GKE cluster and only installs Milvus via Helm.

## Example (for cluster `coco-project`)

```bash
cd milvus-gke

cat > terraform.tfvars <<'EOF'
project_id   = "nih-cl-odss-yiqingz2o-65d7"
region       = "us-central1"
zone         = "us-central1-a"
cluster_name = "coco-project"
namespace    = "milvus"
EOF

terraform init
terraform plan
terraform apply
```

## Validate

```bash
kubectl get pods -n milvus
kubectl get svc -n milvus
```

## Destroy (only Milvus resources managed by this Terraform)

```bash
terraform destroy
```