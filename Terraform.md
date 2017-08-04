# Terraform

It is the provisioning automation of the infrastructure.
Allows us to write infrastructure as code.

ps: Ansible, Chef, Puppet, Saltstack focus on automating the installation and configuration of software;

Instalation:
- Download the zip in terraform.io;
- Export the path to the unziped file;

- Create IAM admin user acc in aws (This is the user used by terraform)

# Shut down instances after using it!

Created user in aws: terraform

## Commands
All commands should be proceedd by `terraform`
Command | Description
---|---
`plan -out out.terraform` | Exports to `out.terraform` file the changes to be applied
`apply [out.terraform]` | Apply configurations
`destroy` | Destroy instance (So we do not have to pay for it)
`plan` | Show execution plan (without applying it)

## Workflow
- `terraform init`
- Add a user that terraform can use
	- Security > IAM (Access key)
	- Add Admin permission
- Create an EC2 instance
- Create instance.tf
	- Look on https://cloud-images.ubuntu.com/locator/ec2/ for ami;
- `terraform apply`

## Provisioning
- There are 2 ways to provision software on our instances
	- Build own custom AMI and bundle software with the image;
		- Packer is a good call for this;
    - Boot  standardized AMIs, and install software on it;
    	- Use file uploads;
    	- Remote exec;
    	- Use automation tools like Chef, Puppet, Ansible;
    		- Chef is already integrated within terraform;

## Observations
- `vars.tf` file defines which variables will be used;
- `instance.tf` file defines variables regarding the aws_instance;
- `provider.tf` file defines aws access variables based on `vars.tf`;
- `terraform.tfvars` file defines the values of `access_key` and `secret_key` variables used in `provider.tf`. This should not be added to version control;
- The time should be updated
	- `date` in terminal to check;
	- To update: `sudo apt-get install ntpdate ; sudo ntpdate ntp.ubuntu.com`
- When spinning up instances on AWS, ec2-user is the default user for Amazon Linux and ubuntu for Ubuntu Linux;

## Best practices
- Always export the execution plan then apply it to avoid creating infrastructure blindly;