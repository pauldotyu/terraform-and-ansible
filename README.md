# terraform-and-ansible

This repo demonstrates the usage of Terraform for Azure VM provisionong and Ansible playbooks for VM configuration.

In order to run this demo in your local environment, you'll need to have the following installed on your local system:

1. Ubuntu or Windows 10 with WSL 
1. [Terraform](https://www.terraform.io/downloads.html)
1. [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
1. [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)
1. [SSH keypair](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys)

Terraform will use your local Azure CLI login context to deploy to your subscription so make sure you are logged in.

The Terraform file will deploy a Ubuntu 18.04 VM in Azure and invoke the Terraform [`remote-exec`](https://www.terraform.io/docs/provisioners/remote-exec.html) resource to install python on the system (using your local SSH keypair for authentication).

The Ansible playbook command will be executed via the Terraform [`local-exec`](https://www.terraform.io/docs/provisioners/local-exec.html) resource and will use the `inventory_azure_rm.yml` [dynamic inventory file](https://docs.microsoft.com/en-us/azure/developer/ansible/dynamic-inventory-configure?tabs=ansible). This will deploy NGINX to all the VMs in the `example-resources` resource group. Upon completion, you should be able to browse to the default nginx webpage using the public IP. 

To run this demo:

1. Open terminal
1. `terraform init`
1. `terraform plan`
1. `terraform apply`

To verify this demo:

1. Terraform will output the public IP address of the VM
1. Browse to http://<YOUR_PUBLIC_IP>
