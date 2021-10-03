# AWSTerraformEC2

Deploy EC2 instance on AWS with terraform 

$ terraform init

$ terraform plan -out=myplan

$ terraform apply

$ terraform destroy

/*
// static way, just for testing purpose, not recommended always use
// environment variables in order to avoid accidental security key leak
// on VCS like git  

provider "aws" {
  region = "<region selected in aws account>"
  access_key = "<access key from aws account>"
   secret_key = "<secret access key from aws account>"
}
*/

provider "aws" {}

/*
set the aws provider info with environment variables
export AWS_ACCESS_KEY_ID="<access key from aws account>"
export AWS_SECRET_ACCESS_KEY="<secret access key from aws account>"
export AWS_DEFAULT_REGION="<region selected in aws account>"
*/

resource "aws_instance" "myfirstserver" {
  ami = "ami-0c2d06d50ce30b442"
  instance_type = "t2.micro"
  tags = {
    Name = "linux"
  }
}


output "ec2create" {
   value = <<EOT
    AWS terraform for ec2 instance creation :
    
    Name = ${aws_instance.myfirstserver.tags.Name} 
    ami = ${aws_instance.myfirstserver.ami} 
    
    id = ${aws_instance.myfirstserver.id} 
    public ip = ${aws_instance.myfirstserver.public_ip} 

    EOT
}
