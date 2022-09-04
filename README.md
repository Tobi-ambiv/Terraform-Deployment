# DEVOPS Training which includes the following;

#how to Setup Terraform, AWS CLI and Deploy AWS EC2 instance using terraform on Visual Studio Code Editor.


#HOW TO SETUP A GITHUB ACCOUNT

#1. on your browser copy this https://github.com/ and paste
#2. click on sign up
#3. enter your email and create a password
#4. verification ofcourse would be send to your email then verify and you go log in. data "" "name"
#5  to check and create your own repository you can go to the github logi and click on the drop then you see "your repository"



#HOW TO INSTALL TERRAFORM ON YOUR COMPUTER(windows)

#1. Download Terraform on your computer using this link https://www.terraform.io/downloads
#2. Select your Operating systems e.g MacOS, Windows or Linux
#3. for windows select windows and select your windows bit(prefferably 64bit-Amd64)
#4. Download and open the zip file install or extract
#5. go to your local C and search for terraform, right-click on it and click on location
#6. open the location and highlight on the url then copy
#7. open your windows search and type edit
#8. click on edit system variables and go to advance
#9. open the environment variables and select Path
#8. select path and click on edit
#9. select new and Paste the terraform link 
#10. save and close all.
#11. and go to terminal(use --cmd & enter--on your windows search) to confirm by typing terraform version




#HOW TO INSTALL AWS ON YOUR COMPUTER(windows)

#1. Download your AWS CLI using this link https://awscli.amazonaws.com/AWSCLIV2-2.0.30.msi  to download it in your system.   NB-you can also search for recent version from https://awscli.amazonaws.com
#2. install and to confirm your AWS version
#3. Open your terminal and type -----  aws --version




#SETTING UP TERRAFORM AND AWS CLI ON VSCODE

#1. Download your VSCode Editor using this link https://code.visualstudio.com/download to your windows computer
#2. Create a folder on your desktop with name Project
#3  Open the Visual Studio Editor 
#4  Open the folder then look for the Folder you created on your desktop and open
#5  look for extension on the left side menu bar and open extension
#6  Search for Hashicorp Terraform and install, on completion of the insttalation, close it and back to extension
#7  Search for AWS CLI and install,  on completion of the installation, close it
#8  Open your terminal  using "ctrol + ~" on your vsccode
#9  confirm your terraform version on your system using    terraform version
#10 confirm your AWS version on your system using       aws --version
#10. on the Terminal beneath the coding space, click on the drop down beside the powershell and select "Git Bash". this will enable you run some linux commands on the terminal
#11. Create file inside our Folder using  touch main.tf   main is the name of our new terraform file. "tf" simply means its a terraform file
#12. link your github account to your vscode by clicking on on the vscode account logo and use your login details to automate


#WRITING AND DEPLOYING AWS EC2 INSTANCE USING TERRAFORM CODES ON VSCODE EDITOR

#HOW TO SETUPN AN AZURE DEVOPS ACCOUNT AND APPLY FOR PARRALELISM

#!. Create a free Outlook account using the link  https://outlook.live.com
#2. open the azuredevops platform using the link https://azure.microsoft.com/en-us/services/devops/
#3. start free/sign up with the Outlook account created
#4. then sign iazure devops with this link https://dev.azure.com/
#5. Create an organization with a unique name
#6. apply for parralelism with the link  https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR63mUWPlq7NEsFZhkyH8jChUMlM3QzdDMFZOMkVBWU5BWFM3SDI2QlRBSC4u




#WRITING AND DEPLOYING AWS EC2 INSTANCE USING TERRAFORM CODES ON VSCODE EDITOR

#1. Create your AWS account and log into the console
#2. 
#1. Open your Vscode
#2. Open the Project folder created on your desktop
#3. Open the main.tf file created in it
#4. 


provider "aws" { #this means we are using aws platform as our cloud provider
    access_key ="${var.aws_access_key}" #this is our aunthetications to be created from thje aws console
    secret_key ="${var.aws_secret_key}"
    region     = "${var.region}"    #this means the location of where we want to deploy and can be found at the top right corner of our aws cxonsole
}


#this is used to create the image file
resource "aws_instance" "ec2-instance" {
  ami           = "ami-090fa75af13c156c2" #this id will be coppied from the console
  instance_type = "t2.micro"
  tags = {
    Name = "Terraform-Ec2_Instance"
  }
}


resource "aws_security_group" "TF_SG" {
  name        = "TF_Seecurity_group"
  description = "TF_Security_group_using_aws"
  vpc_id      = aws_vpc.main.id

  ingress {
    description      = "https"
    from_port        = 443
    to_port          = 443
    protocol         = "tcp"
    cidr_blocks      = [aws_vpc.main.cidr_block]
    ipv6_cidr_blocks = [aws_vpc.main.ipv6_cidr_block]
  }

  ingress {
    description      = "http"
    from_port        = 80
    to_port          = 80
    protocol         = "tcp"
    cidr_blocks      = [aws_vpc.main.cidr_block]
    ipv6_cidr_blocks = [aws_vpc.main.ipv6_cidr_block]
  }

  ingress {
    description      = "ssh"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = [aws_vpc.main.cidr_block]
    ipv6_cidr_blocks = [aws_vpc.main.ipv6_cidr_block]

  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }

  tags = {
    Name = "TF_Seecurity_group"
  }
}

#this code is for creating the storage, s3_bucket is a storage on ec2 and confuring it with the versioning and the acl
resource "aws_s3_bucket" "first_bucket_01" {
  bucket = "tobifirstbucket"
}

resource "aws_s3_bucket_versioning" "versioning_bucket" {
  bucket = aws_s3_bucket.first_bucket_01.id
  versioning_configuration {
    status = "enabled"
  }
}

resource "aws_s3_bucket_acl" "acl_bucket" {
  bucket = aws_s3_bucket.first_bucket_01.id
  acl    = "private"

}

# to run this terraform code on AWS
#1. format the tf code using       terraform fmt     to beautiful the code
#2. type the command   terraform init     to initialize the terraform backend configuration
#3. use the command    terraform plan      to transform the code to frontend configuration 
#4. then the command   terraform apply     to deploy it on amazon web server
#5. use the command     terraform destroy     to cleanup when ou are done so as not to attract charges]

