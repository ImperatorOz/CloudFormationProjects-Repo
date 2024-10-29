# AWS VPC CloudFormation Template

This CloudFormation template creates a complete Virtual Private Cloud (VPC) infrastructure in AWS with both public and private subnets. The template is designed to provide a secure and scalable network foundation for your AWS resources.

## Architecture Overview

The template creates the following resources:
- VPC with DNS support enabled
- Internet Gateway
- 1 Public subnet in us-east-1a
- 1 Private subnet in us-east-1a
- Separate route tables for public and private subnets
- All necessary route table associations and routes

### Network Details
- VPC CIDR: 10.0.0.0/16
- Public Subnet CIDR: 10.0.1.0/24
- Private Subnet CIDR: 10.0.2.0/24

## Prerequisites

- AWS Account
- AWS CLI configured with appropriate permissions
- Basic understanding of AWS VPC concepts
- Access to AWS CloudFormation

## Quick Start

1. **Deploy via AWS Console:**
   - Log in to AWS Console
   - Navigate to CloudFormation
   - Click "Create Stack"
   - Choose "Upload template file"
   - Upload this template
   - Follow the prompts to create the stack

2. **Deploy via AWS CLI:**
   ```bash
   aws cloudformation create-stack \
     --stack-name my-vpc-stack \
     --template-body file://template.yaml
   ```

## Resources Created

### VPC
- Enables DNS hostnames and DNS support
- Tagged with name "MyVPC"

### Internet Gateway
- Attached to the VPC
- Tagged with name "MyInternetGateway"

### Subnets
- **Public Subnet:**
  - Located in us-east-1a
  - Auto-assigns public IPs
  - Tagged with name "MyPublicSubnet"
  
- **Private Subnet:**
  - Located in us-east-1a
  - No auto-assign public IPs
  - Tagged with name "MyPrivateSubnet"

### Route Tables
- **Public Route Table:**
  - Associated with public subnet
  - Includes route to Internet Gateway
  
- **Private Route Table:**
  - Associated with private subnet
  - No route to Internet Gateway

## Template Outputs

The template provides the following outputs for reference:
- VPC ID
- Public Subnet ID
- Private Subnet ID
- Public Route Table ID
- Private Route Table ID
- Internet Gateway ID

## Security Considerations

- Private subnet resources have no direct internet access
- Public subnet resources can access the internet via the Internet Gateway
- Consider adding Network ACLs and Security Groups as needed
- Evaluate the need for NAT Gateway if private subnet resources need internet access

## Customization

To customize this template:
1. Modify CIDR ranges as needed
2. Change Availability Zones to match your region
3. Add additional subnets if required
4. Adjust tags to match your naming convention

## Cost Considerations

Most VPC components are free, but be aware of:
- Data transfer costs
- NAT Gateway costs (if added)
- VPC endpoints costs (if added)

## Limitations

- Template creates resources in a single Availability Zone
- No NAT Gateway included for private subnet internet access
- Basic networking setup without additional security layers

## Best Practices

- Always use private subnets for sensitive resources
- Implement proper security groups and NACLs
- Consider multi-AZ deployment for production workloads
- Follow AWS Well-Architected Framework guidelines

## Support

For issues and feature requests:
1. Check AWS CloudFormation documentation
2. Review AWS VPC documentation
3. Contact AWS Support if needed

## License

This template is available under the MIT License. Feel free to modify and distribute as needed.