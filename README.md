# How to configure AWS CLI for temporary credentials.

## Introduction

To improve security in the use of AWS CLI. Is good idea to always use temporary credential obtained trough the use of MFA. In this way a lost of long term credentials will give more time to containe the damage.

## High level procedure

We will create an IAM user with no policy attached and a 2 factor authenticathion enable. Then this user will be assigned to a group with two policies. One that enforces the MFA and a another that asign the user to an IAM role with all the desired privilegues. 

I have included in this project a cloud formation template called mfa-template.json that creates one user, one role, and one group. The only remaining thing is to register a MFA device and create an acceess key and follow steps 4 to 7. 

## Detailed instructions.

### Step 1
Create an IAM role and attach the desired policies. You can create the role following the instructions in this link: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html#roles-creatingrole-user-console

### Step 2
Create a IAM group and attach the inline policies: AdminMFAPolicy and AllowAssumeAdminMFAPolicy. In the policy AllowAssumeAdminMFAPolicy replace "<role ARN>" with the role ARN you just created in the previous step.

### Step 3
Create a IAM user with only programatic access and asign it to the IAM group created in step 2. 

### Step 4
Generate an Access key ID and Secret access key. You will need them to request the temporary token. 
You can find intructions in this link: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console

### Step 5
Enable MFA authentication in the IAM user account. I'm using Google Authenticator. My Feitian e-pass key doesn't work.

### Step 6
Set your aws cli  profile with "aws configure" and the Access key ID and Secret access key. 

### Step 7
modify the file get_token and replace <role ARN> with the role ARN and <MFA Serial ARN> with the "Assigned MFA device" arn of the IAM user.
  
## How to get the token.
To get the temporary credentials just type "source get_token <code>" where code is the current 6 digit code obtained from google authenticator or your MFA key.
  
I your token is expired or invalid to get new token type "source get_token" to clean the current credentials and then "source get_token <code>" again.
