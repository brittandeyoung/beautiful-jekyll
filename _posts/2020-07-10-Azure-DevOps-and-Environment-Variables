---
layout: post
title: Azure DevOps and Environment Variables
subtitle: The trick to Azure DevOps environment varialbes
tags: [Azure, DevOps]
comments: true
---

My first exposure to Azure DevOps was creating a Terraform pipeline to deliver infrustructure as code to our company's AWS account (Yes I know we are using an Azure Product for pipelining, but deploying to AWS).
When it came time to pass environment varialbes into terraform that were stored in an Azure pipeline library group, I had to do some debugging to figure out why it was not working as expected. 
Hopefully this article will save someone else the troubleshooting time and allow for a quicker first start with the applicaiton. 

I created my first pipeline to run a terraform plan and apply and it was very straight forward using the plugins that are available on Azure Devops. I did start running into issues when declairing a variable in my terraform files. 
We wanted to have some central variables in groups so that any pipeline that needs them could simply add them in the YAML pipeline file. 
I found in the terraform documentation that if you make an environment variable that starts with "TF_VAR_" and the rest mathes the variable name decalired in the terraform file, terraform would simply pull in this environment variable and assign it to the variable at run tinme. 
What happenedon the first pipeline run after defining the variables? The pipeline hung on the terraform plan waiting on the varialbe input. I was puzzled as I made sure to name the varialbe the same in the terraofrm file and in the variable library group, so I started to troubleshoot.
After adding steps in the pipeline to echo out current environment variables, I quickly found the issue. **Azure pipelines will make all environment variables as all uppercase letters, regaurdless of the casing you set in the varialbe name.** 
I had used lower case letters in both the environment variable defenition and in my terraform file. After changing the casing of the varialbe in the terraform file to all uppercase, the variable was pulled in as expected! 
Now I always use all upercase when creating environment varialbe names to avoid potential confion for other team members. 

Hopefully this helps someone. 
