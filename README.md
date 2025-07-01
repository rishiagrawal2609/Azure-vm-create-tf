# Azure VM Terraform Configuration

This Terraform configuration creates a complete Azure VM setup including:
- Resource Group
- Virtual Network and Subnet
- Public IP Address
- Network Security Group (with SSH and HTTP access)
- Network Interface
- Linux Virtual Machine (Ubuntu 18.04 LTS)

## File Structure

- `main.tf` - Main Terraform configuration with resources
- `variables.tf` - Variable declarations
- `outputs.tf` - Output declarations
- `terraform.tfvars` - Variable values
- `README.md` - This documentation

## Prerequisites

1. **Azure CLI** installed and authenticated
2. **Terraform** installed (version 1.0+)
3. **Azure Subscription** with appropriate permissions

## Setup Instructions

### 1. Authenticate with Azure
```bash
az login
az account set --subscription "your-subscription-id"
```

### 2. Configure Variables
Edit the `terraform.tfvars` file and update the following:
- `admin_password`: Set a secure password for the VM
- `location`: Change to your preferred Azure region
- `resource_group_name`: Customize the resource group name
- `vm_name`: Customize the VM name

### 3. Initialize Terraform
```bash
terraform init
```

### 4. Review the Plan
```bash
terraform plan
```

### 5. Apply the Configuration
```bash
terraform apply
```

### 6. Connect to Your VM
After successful deployment, you can connect to your VM using SSH:
```bash
ssh azureuser@<public_ip_address>
```

## Configuration Details

### VM Specifications
- **Size**: Standard_B1s (1 vCPU, 1 GB RAM)
- **OS**: Ubuntu 18.04 LTS
- **Disk**: Standard_LRS (30 GB default)

### Network Configuration
- **Virtual Network**: 10.0.0.0/16
- **Subnet**: 10.0.1.0/24
- **Public IP**: Dynamic allocation
- **Security Rules**: SSH (port 22) and HTTP (port 80) allowed

### Security Notes
- The admin password is stored as a sensitive variable
- Consider using SSH keys instead of passwords for production
- Review and restrict the security group rules as needed

## Cleanup
To destroy all resources:
```bash
terraform destroy
```

## Outputs
After deployment, Terraform will output:
- `public_ip_address`: The public IP of your VM
- `vm_name`: The name of the created VM
- `resource_group_name`: The resource group name

## Customization
You can customize the configuration by modifying the following:

### In `terraform.tfvars`:
- `vm_size` - Change VM size (e.g., "Standard_B2s", "Standard_D2s_v3")
- `os_disk_size_gb` - Change OS disk size
- `vnet_address_space` - Modify virtual network address space
- `subnet_address_prefixes` - Modify subnet address prefixes
- `enable_ssh` - Enable/disable SSH access
- `enable_http` - Enable/disable HTTP access

### In `main.tf`:
- OS image (modify `source_image_reference` in the VM resource)
- Additional security group rules
- Custom scripts or extensions 