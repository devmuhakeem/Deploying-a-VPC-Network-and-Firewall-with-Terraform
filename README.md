# Deploying-a-VPC-Network-and-Firewall-with-Terraform
# Deploying a VPC Network and Firewall with Terraform

A hands-on Google Cloud lab where I used Terraform and Cloud Shell to provision a VPC network and firewall rules as infrastructure as code, instead of clicking through the console.

## Scenario
A fictional bank needed network infrastructure provisioned for a new banking application, and wanted it defined in a repeatable, version-controlled way rather than manually configured. My job was to use Terraform to build the network and firewall.

## What I did

### 1. Set up Terraform in Cloud Shell
Installed the Terraform CLI via the HashiCorp apt repository and configured it to persist across Cloud Shell sessions, then verified the install with `terraform --version`.

### 2. Cloned and reviewed the Terraform configuration
Cloned a Terraform example repo into Cloud Shell and inspected `main.tf` to understand what it would provision:
- A firewall rule allowing ICMP and TCP traffic on ports 80, 8080, and 1000–2000
- A new VPC network, with both resources using a dynamically generated unique name suffix to avoid naming collisions

### 3. Deployed the infrastructure
Set the target project, then ran:
```
terraform init
terraform apply
```
Confirmed the plan and applied it, resulting in 3 resources created — the VPC network, the firewall rule, and a supporting resource.

### 4. Verified the deployment
Went into the VPC networks page in the console and confirmed the new `test-network` existed alongside the default network, then checked its firewall rules matched exactly what was defined in `main.tf` — same ports, same protocols, same action.

## Key takeaways
- Infrastructure as code turns firewall and network changes into something reviewable and repeatable, instead of manual console clicks that are hard to audit later
- Reading `main.tf` before running `apply` matters — you should know exactly what Terraform is about to create before you approve it
- Verifying the deployed resources against the source configuration closes the loop: the code isn't just declarative, it's provably what got deployed

## Tools
Terraform, Google Cloud Shell, VPC Firewall, Compute Engine networking

---
*Completed as a Google Cloud Skills Boost lab.*
