> Credit: https://gitlab.com/cloudformation/tutorial

# CFN Tutorial & Best Practices

Welcome to the guide. This guide will attempt to quickly help you use AWS Cloudformation, define some of the best practices and caveats and then lead you to the rest of the documentation that will help you become an expert in Cloudformation usage.

Where possible, I will try and link to the specific pages in the document that you can read if this guide isn't making sense. 

## Basics
If you're not familiar with AWS, or you haven't done this part, each AWS authored guide has a section on getting started, you might already be an expert however it might also be worth a quick read just to make sure the reader of this guide is in the same place, please have a look at:

http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/GettingStarted.html

## What is Cloudformation?

It can be best described as a tool that helps deploy infrastructure as code. The specific code is JSON formatted and when fed to CloudFormation, will direct it on what resources to create. There are other tools that do this for other products, OpenStack uses Heat (Which can also interface with other platforms), VMWare use vRealize, Azure and GCE even have their own versions but they are not as mature. Users can write templates and deploy them as stacks using the Cloudformation GUI, CLI or API. One of the great benefits of using the tool is that when it comes to cleanup, you can delete the stack and all resources that were created in it will be removed.

Stacks (Created via Templates) can be very simple, maybe a single template that just brings up a few resources like an Ec2 Instance, or they can be incredibly complex and create entire environments from the ground up. In this guide, you'll see how you can start with a simple template and eventually update it to the point of being complex (which should obviously be driven by some purpose, otherwise keep them as simple as possible).

### Template Components

All templates are JSON formated and consist of the following:
Parameters
Mappings
Conditions
Resources
Outputs
The anatomy of which looks like the following:
```sh
{
  "AWSTemplateFormatVersion" : "version date",

  "Description" : "JSON string",

  "Parameters" : {
    set of parameters
  },

  "Mappings" : {
    set of mappings
  },

  "Conditions" : {
    set of conditions
  },

  "Resources" : {
    set of resources
  },

  "Outputs" : {
    set of outputs
  }
}
```
You can view the documentation for the Template Anatomy here:
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html


**NOTE:** One of the most common syntax errors in a template is a missing comma between sibling property declarations and between resources. The other one which isn't mentioned in the manuals is an extra trailing comma after the last resource in a set of braces, which will also cause it to fail.


### Template Limits
Limits are ever changing, whenever new services and updates are released to AWS, limits can change. Some limits can also be changed by asking AWS if you have a valid reason. For Cloudformation specific limits, please check here:
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html


## Template Design
This section is probably the hardest to write becauase the ways in which Cloudformation can be consumed are very broad. What needs to be decided first is the kind of environment that's needed. Sometimes it is sufficient to use only Cloudformation to complete the configuration and deployment of a service.
A scenario here could be that we want to deploy 2 LDAP servers into the VPC that we own, in which case we could configure these purely using Cloudformation, or they could be part of a bigger management stack that would deploy multiple tiers and services, most likely from separate child templates linked together by a parent.

The following steps in this repo are intended as a fast track into seeing how templates and Cloudformation usage can evolve over time. At the beginning of any project most templates are a single file, however over time and with discovery of new options or services that are needed, templates split apart and operate in a Parent/Child model, or become separate entities managed by a higher level orchestration tool, maybe Jenkins.

https://gitlab.com/cloudformation/tutorial/tree/master/step1

https://gitlab.com/cloudformation/tutorial/tree/master/step2

https://gitlab.com/cloudformation/tutorial/tree/master/step3

https://gitlab.com/cloudformation/tutorial/tree/master/step4

If you intend to follow the guide because you can't wait to get your hands dirty, it is worth coming back and reading the rest of this page to understand some of the pitfalls and caveats of using Cloudformation as there are some activities that aren't obvious which can influence the way you deploy, or even break your existing resources.

# Best Practices

Without repeating what has already been written by the subject matter experts, please consider this:
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html

I have commented on each of the segments in terms of experience that we've had and how we used the best practice.

## Organize Your Stacks By Lifecycle and Ownership
In this context, you can have various types of application, service or component that will live in an AWS environment. Initially you might just build a bastion, like in the Step1 of the tutorial above. On it's own that might be pretty useless, however if you're doing it again and again for a project and you need to deploy multiple bastion servers, (or maybe a jumpbox fo developers), then it makes sense to drive it with a template. 
The same resource here could be deployed within a larger stack, or on it's own. For example, if you had a typical dev, test and prod environmet and this bastion happened to be for various Ops people to use for administration and troubleshooting in each environment, you could integrate this into the environment so that it's deployed whenever the platform is. Alternatively, this might be a host that is supplied to each single user and therefore could be deployed by Jenkins, whereby Jenkins will interact with the Cloudformation service to deploy the template. (see this link for more of an example: http://awsbits.blogspot.co.uk/2015/01/jenkins-packer-puppet-and-aws.html)

## Use IAM to Control Access
While this section talks about he benefits of restricting what users can do with CloudFormation, you can also use CloudFormation to provision IAM Resources. IAM Roles are used by instances as a replacement to storing credentials on the host. For example, during the deploy of your first stack (let's call it a management tier), you may have all your configuration files in S3. To access S3, you could use keys/credentials, however that isn't safe to store on your host. The safer way is to create a role that can be applied to the host when it's built. The role will contain 'GetObject' for the bucket that hosts the configuration files allowing the instance to build from config files located in S3.

## Verify Quotas for All Resource Types
There have been a few occasions where limits have been hit and CloudFormation 'CreateStack' functions have failed. It is simple enough to request limit extentions through the console, however it is also good to understand whether limit increases or architectural changes are needed to avoid this scenario. Prior to deploying anything into your VPC, work out what the limits are and whether you have enough headroom. Trusted Advisor can be used to assist with this task, making it easier to find these figures. If there is no access to Trusted Advisor, the same details can be taken from the Ec2 > Limits section of the console.

## Reuse Templates to Replicate Stacks in Multiple Environments
Adding Mappings, Conditions and Parameters to templates mean that you can use a single set (parent/child) of templates to deploy multiple environments in the same region, or even in different region if you make use of mappings to 'find' the correct values for the region.
Here is an example of a condition that uses a parameter to govern the type of instance that will be deployed:

```sh
{
  "AWSTemplateFormatVersion" : "2010-09-09",
  "Description" : "Some stack that does some thing.",

  "Parameters" : {
    "StackType" : {
      "Description": "Allowed values are 'dev', 'qa' or 'prd'. You must specify the stack type.",
      "Type": "String",
      "AllowedValues" : ["dev", "qa", "prd"]
    }
  },

  "Conditions" : {
    
    "BuildDev" : {
      "Fn::Equals" : [ { "Ref" : "StackType"}, "dev"]
    },
    
    "BuildQa" : {
      "Fn::Equals" : [ { "Ref" : "StackType"}, "qa"]
    },
            
    "BuildPrd" : {
       "Fn::Equals" : [ { "Ref" : "StackType"}, "prd" ]
    }
  
  },
  
  "Resources": {
    
    "BastionInstance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "KeyName" : { "Ref" : "KeyName" },
        "InstanceType" : 
          { "Fn::If" : [ "BuildPrd", "m3.large",
           { "Fn::If" : [ "BuildQa","m1.small", 
             "t1.micro" 
           ]}
        ]},
        "ImageId" : { "Fn::FindInMap" : [ "ImageMap", { "Ref" : "AWS::Region" }, "BastionAMI" ]},
        "SecurityGroups" : [{ "Ref" : "BastionSecurityGroup" } ],
        "SubnetId" : { "Ref" : "PubNet01" },
        "AssociatePublicIpAddress" : "true",
      }
    }
  }
  
}
```
Here, we're using a function that will allow us to specify the type of environment that we're going to provision, if we're making a 'prd' environment, then the bastion will get an m3.large instance because the 'BuildPrd' condition will be true ('prd'). Think of this like an IF loop, if the BuildPrd condition wasn't true, we move on to the next action, which is another IF statement that asks, 'ok, then is it QA?'. If BuildQa is true, then we get an m1.small instance type and if that condition wasn't met, for all other environments (in this case there is no parameter constraint for StackType, so it could be a value of 'dev' or 'notdev' the instance will be a t1.micro.

Obviously, this isn't necessarily a real world scenario that we'd suggest using for Bastions, but it shows how we can be dynamic about the resource provisioned using a single template for multiple regions and/or environments.

Using mappings in addition to this, you could also run this template in multiple regions by 'Finding' the relevant AMI ID for the region you're working in, like this:

```sh
{
  "AWSTemplateFormatVersion" : "2010-09-09",
  "Description" : "Some stack that does some thing.",

  "Mappings" : {
    
    "ImageMap" : {
      "eu-west-1" : { "NatAMI" : "ami-14913f63", "BastionAMI" : "ami-9d23aeea", "JenkinsAMI" : "ami-9d23aeea", "GitLabAMI" : "ami-9d23aeea", "LdapAMI" : "ami-9d23aeea" },
      "us-west-2" : { "NatAMI" : "ami-290f4119", "BastionAMI" : "ami-dfc39aef", "JenkinsAMI" : "ami-dfc39aef", "GitLabAMI" : "ami-dfc39aef", "LdapAMI" : "ami-dfc39aef" }
    }
    
  },

  "Resources": {
    
    "BastionInstance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "KeyName" : { "Ref" : "KeyName" },
        "InstanceType" : 
          { "Fn::If" : [ "BuildPrd", "m3.large",
           { "Fn::If" : [ "BuildQa","m1.small", 
             "t1.micro" 
           ]}
        ]},
        "ImageId" : { "Fn::FindInMap" : [ "ImageMap", { "Ref" : "AWS::Region" }, "BastionAMI" ]},
        "SecurityGroups" : [{ "Ref" : "BastionSecurityGroup" } ],
        "SubnetId" : { "Ref" : "PubNet01" },
        "AssociatePublicIpAddress" : "true",
      }
    }
  }
}
```

In the case above, we could have run this in us-west-2 and we'd have ended up with ami-9d23aeea as the AMI being used for the bastion, if we'd used eu-west-1, we'd have been using ami-dfc39aef. These images are identical but they are bound to the region they're in, so when you're making templates that are required to run in multiple regions the AMIs need to be replicated.

## Use Nested Stacks to Reuse Common Template Patterns

Rather than repeat what has already been discussed in the blog below, it's definitely beneficial to group your templates:
http://awsbits.blogspot.co.uk/2015/01/basic-cloudformation-template-design.html

At a high level, we've found that we can group in various ways, however the demarcation between doing it in CloudFormation or doing it in a higher level automation tool does help govern template heirarchy. The second paragraph in the AWS best practice goes further and suggests abstracting single functions into a template that is reused by multiple stacks/users, the owner of that template can then update all ELBs in the estate just by updating the single template - which of course means all users of the template will need to be notified as they'll need to update their stacks, unless they're joined in the parent/child examples given in the steps and on the blog post.

Step 2 introduces the condept of using the AWS::CloudFormation::Stack resource:
https://gitlab.com/cloudformation/tutorial/tree/master/step2

## Do Not Embed Credentials in Your Templates
Absolute no no.
Enough said!
But as stated, where it's unavoidable use the NoEcho value to prevent people reading the credential from the CloudFormation Management Console. If a user does get a copy of the templates and you do hard code passwords, they'll be able to read them in plain text. It is far better to never set the default for these fields and only enter them at the point they're needed, whilst using the NoEcho function as well.

## Use Parameter Constraints
Drawing on best practice above, you could use something like this, which uses NoEcho as well as constraints to force the password to be complex.

```sh
"SomePassword" : {
      "NoEcho": "true",
      "Description" : "The database admin account password",
      "Type": "String",
      "MinLength": "8",
      "MaxLength": "41",
      "AllowedPattern" : "[a-zA-Z0-9]*",
      "ConstraintDescription" : "must contain only alphanumeric characters."
},
```

Note there is no default field here. These constraints can be applied to other Paramters, like this Environment Paramter:
```sh
"Environment" : {
      "Description" : "Stack environment",
      "Type": "String",
      "Default": "test",
      "AllowedValues" : ["prod", "test"],
      "ConstraintDescription" : "must specify 'prod' or 'test', no other values are allowed."
},
```

## Use AWS::CloudFormation::Init to Deploy Software Applications on Amazon EC2 Instances
This is a very valuable tool. Initially we attempted to do everything with it, however as time goes by, it's better to find a demarcation point between preparing a system and configuring/installing applications. Take user creation for example, or maybe LDAP database population, or maybe even configuring a Jenkins host, while it is possible to do this in CloudFormation, it can actually be easier and more fruitful if the installation and configuration are moved to more powerful tools like Puppet, Chef or Ansible. The following scenario is one we have tried and tested for an application that needs scaling:

Provision Environment with CFN: AZs, Network Routes, Subnets, Security Groups, IAM Roles, Tags (Tags is the demarcation between the team that provisions the environment and those that provision the app)
Provision the App: Using Jenkins, run a CFN template that uses values from the environment above

Jenkins ties the two work flows together using tags, we can re-deploy the applicaiton again and again into multiple stacks and the only change is the DNS/LoadBalancer entry point for the applicaiton. 

## Validate Templates Before Using Them
This goes without saying really. Most people usually start with the Console, which automatically verifies the template after putting in the parameters and before actually building/updating a stack. Refere to this page for the usage of the CLI:
http://docs.aws.amazon.com/cli/latest/reference/cloudformation/validate-template.html

## Manage All Stack Resources Through AWS CloudFormation
This is very important!

If you try and delete a security group (as an example) and it has another host using it that is not controlled by CloudFormation, when you try and delete the action will fail, sometimes this is catastrophic and you will be left with the 'ROLLBACK FAILED' condition, see why that's so bad here:
http://awsbits.blogspot.co.uk/2014/08/the-dreaded-updaterollbackfailed.html

Whenever you want to add or remove anything from a stack/environment, it is best to do it with CloudFormation. This subject looks toward your design choices for the demarcation between using CloudFormation and other higher level automation tools, such as Jenkins. As an example, if you manage security groups and subnets in CloudFormation, you shouldn't begin provisioning them in some other way (manually, or via Jenkins), unless you plan to migrate the strategy for creating them entirely.

## Use Stack Policies
Using Stack Policies is another way to protect the environment that you have built using CloudFormation from accidental change or attempted deletion. For example, if your environment uses an RDS backend (msyql or postresql) which you need constantly available (multiple AZ) and backed up (db snapshots), which is managed by a separate team and provisioned by the Ops guys in your team, it is good to protect this from any accidental changes when you begin allowing other members of the organisation to run CloudFormation tasks using an upstream tool, such as Jenkins. Although it would take quite a bit of imagination to do damage to the underlying CloudFormation controlled environment if you have permissions set correctly for other resources, it is still possible, so these policies give it a little extra protection.

As per the documentation, follow the links in the best practices page and read about how to do it.

## Use AWS CloudTrail to Log AWS CloudFormation Calls
In and of itself, come audit time CloudFormation templates are excellent support for providing a picture of what is and isn't installed/permitted. As CloudFormation is adopted throughout the business and it's used across all all teams in different ways, this tool will assist in tracking who makes the changes. This tied together with other audit trails will produce information on every action ever taken against a stack, which can be vital in Audit, issue troubleshooting, triage and security breach.

## Use Code Reviews and Revision Controls to Manage Your Templates
Finally, put the templates in a Revision Control System. Make sure you can check out, check in and branch the code, just like you would for any software application, that way you can operate in the same way, making smaller changes more often as well as having all previous known versions of the architecture and all changes that have been made.


# Tutorials
Now you're armed with a bit of background on CloudFormation and how it can be used, it's worth following the examples to get the feel for creating stacks. Start with Step1 that creates a simple Amazon Linux Instance and allows you to connect to it via SSH.
