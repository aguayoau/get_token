# How to configure AWS CLI for temporary credentials.

## Introduction

To improve security in the use of AWS CLI. Is good idea to always use temporary credential obtained trough the use of MFA. In this way a lost of long term credentials will give more time to containe the damage.

This project is based in the blog https://www.jeffgeerling.com/blog/2018/getting-aws-sts-session-tokens-mfa-aws-cli-and-kubectl-eks-automatically

## High level procedure

We will create an IAM user with no policy attached and a 2 factor authenticathion enable. Then this user will be assigned to a group with two policies. One that enforces the MFA and a another that asign the user to an IAM role with all the desired privilegues. 

## Detailed instructions.

1. Create an IAM role and attach the desired policies. You can create the role following the instructions in this link: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html#roles-creatingrole-user-console

2. Create a IAM group and attach the inline policies: AdminMFAPolicy and AllowAssumeAdminMFAPolicy. In the policy AllowAssumeAdminMFAPolicy replace "<role ARN>" with the role ARN you just created in the previous step.

Create a IAM user with only programatic access. You can find intructions in this link: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console

2. 
