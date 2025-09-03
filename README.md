Introduction:
The repository contains the deliveries for the home task by Mars.
The repository contains the following folders:
- helm : contains the helm chart with the application yaml templates that is handled by ArgoCD
- Prometheus : contains the Prometheus files   ______
- Terraform : Contains the terraform code to be downloaded and run using Terraform CLI

Assumptions:
- Since it's a demo, the cheapest chipset was chosen, without considering redudency or stability
- For the same reason, the self sign was chosen (instead of real DNS)
- For simplicity, the deplyment is done by a user with permissions and not by assume role.
- Password encrytption is not handled in this task

Prerquisites:
- An AWS user with the following permissions _____
- Terraform CLI installed locally
- AWS CLI installed locally
- kubectl component installed locally


Running instructions:
1. Download the Terraform folder
2. Run command "aws configure" and insert user credtentials
3. Run command "cd create_cluster"
4. Run command "terraform init"
5. Run command "terraform plan" and verify there are no errors
6. Run command "terraform apply -auto-approve"
7. Wait for run to complete
8. Run command "cd ../apply_components"
9. Repeat steps 4.-7.
10. Run command 
