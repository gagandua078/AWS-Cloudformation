# CorpWeb CloudFormation Template

## Overview

This repository contains the CloudFormation template `corpweb.json`, designed to automate the deployment of a highly available web application infrastructure on AWS. The template provisions a VPC, two public subnets across different Availability Zones for high availability, two Amazon Linux EC2 instances for hosting the web application, an Application Load Balancer (ALB) to distribute incoming traffic, and necessary security groups.

## Architecture

- **VPC**: `EngineeringVpc` with CIDR `10.0.0.0/18`.
- **Subnets**: Two public subnets (`PublicSubnet1` and `PublicSubnet2`) in different Availability Zones for redundancy.
- **EC2 Instances**: Two instances (`WebServer1` and `WebServer2`) running Amazon Linux 2, auto-configured with HTTPD and PHP, demonstrating a basic web server setup.
- **Application Load Balancer (ALB)**: `CorpWebALB` distributes incoming HTTP traffic across the two instances.
- **Security Groups**: A security group `WebserversSG` that allows SSH access from a specified IP and HTTP access from the internet.

## Prerequisites

- AWS Account and AWS CLI installed and configured.
- An existing EC2 Key Pair in the target AWS region.
- Knowledge of your public IP address for secure SSH access configuration.

## Deployment Instructions

1. **Clone the Repository**: Clone this repository to your local machine or download the `corpweb.json` file directly.

    ```bash
    git clone https://github.com/yourusername/corpweb-cf-template.git
    cd corpweb-cf-template
    ```

2. **Deploy via AWS CLI**:

    Replace `<YOUR-KEY-PAIR-NAME>` with your actual EC2 Key Pair name and `<YOUR-IP-ADDRESS>` with your public IP address in CIDR notation. Then run:

    ```bash
    aws cloudformation create-stack --stack-name CorpWebStack --template-body file://corpweb.json --parameters ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyPair,ParameterValue=<YOUR-KEY-PAIR-NAME> ParameterKey=YourIp,ParameterValue=<YOUR-IP-ADDRESS>/32 --capabilities CAPABILITY_IAM
    ```

    This command will create a new CloudFormation stack named `CorpWebStack` using the template.

3. **Monitor Deployment**:

    Use the AWS Management Console or AWS CLI to monitor the stack creation process. Once the stack status is `CREATE_COMPLETE`, find the ALB DNS name in the Outputs section.

4. **Access Your Web Application**:

    Navigate to the ALB DNS name using any web browser to access the deployed web application.

## Clean Up

To avoid incurring future charges, remember to delete the CloudFormation stack once it's no longer needed:

```bash
aws cloudformation delete-stack --stack-name CorpWebStack

```
--

## License

The code within this project is dual-licensed under the GLINCKER LLC proprietary license and the MIT License. This means it is open for reference and educational purposes, allowing for use, modification, and distribution in accordance with the MIT License's terms, while also respecting the proprietary rights and restrictions under the GLINCKER LLC license.

## MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
