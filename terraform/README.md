# Terraform
The configuration file `gcp.tf` is based on [Terraform container cluster documentation](https://www.terraform.io/docs/providers/google/r/container_cluster.html). The following steps are required to deploy the cluster in [GKE]((https://cloud.google.com/kubernetes-engine/)) (assuming you already have [Terraform locally](https://www.terraform.io/downloads.html), don't you?).

1. First, you need to create and download
[Google service account key](https://console.cloud.google.com/apis/credentials/serviceaccountkey).
Save as `gcp.json`.

2. Create a file called `gcp.tfvars` using your own data: project and region/zone to deploy ([see the list](https://cloud.google.com/compute/docs/regions-zones/)), a new  username/password pair to login to K8s dashboard. Use this format:
```
gcp_project = "<insert your project here>"
gcp_zone = "<insert your zone here>"
gke_username = "<insert your GKE username here>"
gke_password = "<insert your GKE password here>"
```
Just a note: if you choose region instead of zone, GKE will create workers on ALL zones, multiplying by this factor the number of nodes.

3. Initialize working directory:
```bash
terraform init
```

4. Create the execution plan:
```bash
terraform plan -var-file=gcp.tfvars
```

5. Apply to achieve desired state (it takes about 1-2 min):
```bash
terraform apply -var-file=gcp.tfvars
```

6. Optionally, show up the current state:
```bash
terraform show
```
