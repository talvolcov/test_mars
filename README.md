Introduction:
The repository contains the deliveries for the home task by Mars. 
The Environment is designed to be deployed on AWS and contains the following components:
Kubernetes cluster with a guestbook application (as attached to the task), Ingress controller with Cert-manager, ArgoCD and Prometheus/Grafana.
All the environment will be deployed by a single run of Terraform code.
The following folders are located in the repository:
- helm : contains the helm chart with the application yaml templates that is handled by ArgoCD
- Terraform : Contains the terraform code to be downloaded and run using Terraform CLI

Assumptions:
- Since it's a demo, the cheapest chipset was chosen, without considering redudency or stability
- For the same reason, the self sign certificate was installed (instead of real DNS). The access to the website will trigger a validation error, but checking the certificate detail will provide the DNS name
- For simplicity, the deplyment is done by a user with permissions and not by assume role
- The deployment should be done with admin access (sorry, but I didn't find a convenient way to narrow permissions)
- Password encrytption is not handled in this task

Prerquisites:
- An AWS user with the admin access.
- Terraform CLI installed locally
- AWS CLI installed locally
- kubectl component installed locally


Running instructions:
1. Download the Terraform folder
2. To run terraform code for the environment deployment:
  a. Open terminal 
  b. Run command "aws configure" and insert user credtentials
  c. Run command "terraform init"
  d. Run command "terraform plan" and verify there are no errors
  e. Run command "terraform apply -auto-approve"
  f. Wait for run to complete
4. To enable access to the websites, the following actions need to be done:
   a. To adjust context, run command "aws eks --region us-east-1 update-kubeconfig --name mars-task-cluster"
   b. To receive the cluster URL run command "kubectl get svc -n ingress-nginx ingress-nginx-controller -o jsonpath='{.status.loadBalancer.ingress[0]}'"
   c. Copy the URL from the result and use it in the command "nslookup { result_url }"
   d. The output should be 2 public IPs (under "Adresses" section)
   e. Copy one of the public IPs to a new line in your hosts file on your computer as follows:
   {copied public ip}  guestbook.local argocd.local prometheus.local  grafana.local
   f. Save the file



Environment access:

Guestbook application- Browse to URL "https://guestbook.local" and test the UI
ArgoCD: 
1. Browse to URL "https://argocd.local"
2. Enter credentials: admin / ArgoCD_pass!
3. Inspect details

Prometheus - Browse to URL "https://prometheus.local" and test the UI

Grafana: 
1. Browse to URL "https://grafana.local"
2. Enter credentials: admin / Grafana_pass!
3. Inspect details 
