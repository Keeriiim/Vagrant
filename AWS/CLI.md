- [IAM](#iam)
- [Configuration](#configuration)
- [Commands](#commands)
- [Troubleshooting](#troubleshooting)

# IAM
- You first need to have an IAM account.
- Create user
- Attach policy  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/b8f2f9f5-d509-4465-bc84-f266752a72b3)  

![image](https://github.com/Keeriiim/Vagrant/assets/117115289/c501ad87-50e2-4651-bcb1-924dcaae7f13)  

## Access Keys
- Find the user -> Security credentials -> Create access key  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/7d48a67b-cace-4eb2-ab7d-3336c867c184)

- NEVER STORE YOUR KEY ONLINE!, this is only for documentation
- Once created, you will only be able to see it/download the csv file once. But you can deactive / delete it.  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8eac5cf7-0459-488e-8fce-57395fbe10da)

```bash
@cc€ss key:
AKIA2UC3F56EWFM34LOH

Secret @cc€ss key:
+MMXegvaLFQE3oRyYk2UnFVIYdEqGQ/OisKaLL/Q
```

# Configuration
- [Read](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
- Open bash
```bash
aws configure
AWS Access Key ID [None]: AKIA2UC3F56EWFM34LOH
AWS Secret Access Key [None]: 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
Default region name [None]: us-east-1
Default output format [None]: json
```

- You can access / change credentials 
```bash
ls ~/.aws/
config  credentials

kerim@DESKTOP-KUF81S4 MINGW64 ~
$ ls ~/.aws/credentials
/c/Users/kerim/.aws/credentials

kerim@DESKTOP-KUF81S4 MINGW64 ~
$ cat /c/Users/kerim/.aws/credentials
[default]
aws_access_key_id = AKIA2UC3F56EWFM34LOH
aws_secret_access_key = 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

```



# Commnads
- Create sg
```bash
aws ec2 create-security-group --group-name cli-sg --description "created from cli"
```

- Show all sg 
```bash
aws ec2 describe-security-groups --group-names
```

- Create inbound rule
```bash
curl https://checkip.amazonaws.com # Your ip will be without /32 so you have to add it
$ aws ec2 authorize-security-group-ingress --group-id sg-083cbc022c483a22d --protocol tcp --port 22 --cidr 78.82.182.26/32 # Custom for SSH connection
aws ec2 authorize-security-group-ingress --group-id sg-083cbc022c483a22d --protocol tcp --port 80 --cidr 78.82.182.26/32
```


- Show running instances
```bash
aws ec2 describe-instances
```

- Create running instances
```bash
# You need to know image-id and type
aws ec2 run-instances --image-id ami-080e1f13689e07408 --count 1 --instance-type t2.micro --key-name RSA_Key --security-groups cli-sg
```

- Create key-pair
Creates the key inside current folder!
```bash
 aws ec2 create-key-pair --key-name RSA_Key --query 'KeyMaterial' --output text > RSA_Key.pem
```

- Create tags
```bash
 aws ec2 create-tags --resources i-07b443e9f33d1101b --tags Key=Main,Value=webbserver # You need to know the id
```


- Delete instance
```bash
aws ec2 terminate-instances --instance-ids <Instance-Id>
```

- Create tags
```bash
 aws ec2 create-tags --resources i-07b443e9f33d1101b --tags Key=Main,Value=webbserver # You need to know the id
```

- Create tags
```bash
 aws ec2 create-tags --resources i-07b443e9f33d1101b --tags Key=Main,Value=webbserver # You need to know the id
```

- Create tags
```bash
 aws ec2 create-tags --resources i-07b443e9f33d1101b --tags Key=Main,Value=webbserver # You need to know the id
```




# Troubleshooting
- When a commands fails u get an encrypted message.
```bash
aws --version
aws sts decode-authorization-message --encoded-message "your-encoded-message"
```

```bash
$ aws ec2 run-instances --image-id ami-080e1f13689e07408 --count 1 --instance-type t2.micro --key-name RSA_Key --security-groups cli-sg                                  
An error occurred (UnauthorizedOperation) when calling the RunInstances operation: You are not authorized to perform this operation. User: arn:aws:iam::730335670153:user/admin is not authorized to perform: ec2:RunInstances on resource: arn:aws:ec2:us-east-1:730335670153:instance/* with an explicit deny in an identity-based policy. Encoded authorization failure message: ifwWlz-OIMBLKmkLR-0zrVvhLuwCjvORcWmFlWf3ZlsUDIBqg0z5kYTCUqwpRlBHHQW3LpThM0GnS69ByyXh-zKmOYlLv9s3m-iihj--9uTd5hQRNChFxv5vVM_xFfWusw-un-StcnI65HNOxPzpSwVKjfIOk8bdjzrUrJmrEVMaEmE5zXTMoilCQV-7VCwk4tOickhsvHM14E31woA2DcC5c2seAXAvUf5MlMNbtvdOw3jVsoYWl-Pc1Ky0qNXZFBX0cgFzF7j_Jfx6b5DGAW9VzmR5qGncHqXOvPZqtNLQPi2F5FQs_yUF3ZIv4rQ0kAJsdX0Gy891TOCSA8o_veKKt4fNOurAaVFFboE9MVzIdSF-E0Oo3ciP1KCRWdumtpCDHfmyL7zRGOr6ORW_BwiGZNWaG6Rx2NUv3OigaR5hNMqFMxGPLkHAXyRNJ2gQ03jk4cp0qURGkw-GtZqY-_GDExORkqj57_z_bbUX2hP_WdnlLChYhusNn2HflbINnvykD3PpaIfOipzav3pxJ-rhvTZh-Q7jRIN1emFMTmOOAotprzMBeEiCGEic9XNn4JYFC-PsWhpadoI2T5ZUINU1qchoKqX5SjoO8DgyFCBNoW3o8kfq-26sOlx_x9_nyI3HE9I5iNpADS7nI001TsqpPmQW5dk5yNcgX6WzQ_1JmpevXs6i0NPHie--1ch6hHfJkDuTQG61tMzj7cjov-DtLshRR7r1UrafSkG2iCKcm3AUgxUuRNiVIGflhOYBWDRUjjJ4vLu0B75GxkEvuXeWpMBHbPSi1fz6GvUL3V0LHnFRnctMGroC7-Sa6yDqfUYyIoQZi-2T0EWiydP-41efVtJR3zAcx6ke4ci5CPViWglK8WkUYvxDE8praM3N80JZ5c7saMOy4ZCCLn2DjjakMtUCeE1ax3EJ7ZXZ9wspd-mnDpPCnzdhg0X4GsRNNxfpmo5UJ8HmuV5N01gDf6k1vjpFWbsww2SI2ipMz9nLNTl6a7WyM6uUnD7FQ4xY-B0FP9nLB83yWSx_JzNBF_8HDWs0Zw0uf3PFWaFm-nBIdkhJvJmLFD53-CSe13dnQnIWKSHrSj-IfzVxaCOtx3n4oerxcLQrTQtfogB5sSkG7nF2owhOgA9Yx4RmUcSJOLTk-iexrs8zQMUoji8ufZEtwfJ5VnZiSVZKavbn4xzwKEZRGEc6cUWLuWmwBb3Wk4m3pFyPUcA0oHy5ilKdo9NbNpBbXBOaangURV5d2t9Gy-tmtzebUPE3RjxUz_peySZlJ8o9WimGbaaYeTIL3zEQ_eDdHgCI7IhT5y8BMz78kqofXc6kJoT9NA908s7-aU7qtK1MA35vD7jNrUmLaRJwCTK4nUrazomaHV27pwd_2vJxljk0k3mQRuDlN7vim449jjo0XM-jxt943KRM0OZliaNcinwnl6U4-xbfCSPVuPLk862ZMj1QxoaMVkMQmkRiaDc9OyPjkPbd375g3lfFjp0MYHojD5si5II7mfkQVKzNV-5VtMjpNkyvpbE


$ aws sts decode-authorization-message --encoded-message yuM3HDOYAR5X95EXnvYBgeSE0ajku4TT0O01vFI55HG1O4Qgs9hor3H0j95SYiwHYO_nrzqLMwQvEJKtmSv2NlkKLtEQPGO36S7d6MGj56ZFQ2xGtviGOGShh8Fpnm_YFP9RLYR_Tmdo8mqARun8zWAXhfDjr_HC5vGXUDo3auYvDslyNzZy8CtIUYCs4xnqeAwDTlyyR_gmHkdFkJPSai052moRTNPklolL2p1Mk_7sfunpTfunYj2M59QPII6GUEFCGPL0dx-QdKDRGfkkoiL-Q8yZ1YHMuY-4sx0p54guC9HfeTrzw9pBpryhlgW7s8MquNRUYLgSJRKqLgBTVoZw2wzQKuM4bm-G-f1oUm3ekoLv97RrgJQPn9DvDN2wOAiSy8zNujspI7UgHl-szTTUkPCSjq9vDLk7zXotYvmQKi_e6_YWN566ZcqBcpPfr8qnKsW0d_tnd4B6QLdup7y_hbFwl0owAhobPlGQkSO8OV5CTeyexrrULkpAvz-Q6AgbEhV5tc1G68r15gVXMVecInOjSDGpi-yrWsVeFsAQHAD0Vx6EZbNYS1URdoUi0C5i4uCXPXHXRTeFNFOFKZ3HoWwoX2ojMK4L0zUPSrrIeDrQMivtm-4JMG4m1SNF92ZgO-cv6AXtgJ8L2ZglOu6XSd35dxTisMS2dTx4YoSfuUN6QsXkq_OINYchDGVIuznO_ONlAcDYOg3G0oq5lhe1jPtie8TjNvxXEHmSN7I0cZm-MoxTzdFwfXVwRbqdKqxiEivOlpgn55Ffso713Wd_3eyoRAyx8-G1mU8pd4Suw6pKBLyOC4iSKtJQZlwuKI-mB-mJrWhpXZqBZpZWCYPBWY7FsSJpkcmh0Y0iaxMzgmL-bSgHeA6HIOAl0HfQuMMK4foNXqQ4-NeP2rYnqCaqVS0ljWFpmQdrOIyAeSxN6rJlVZMSemFn5i1Fo6XM8EotbIZgxhoNBKfwoWxDvEukJmSUFR_VTAPSDVDICgGriY4WVxnCPrnrQ3DBMtjAFacD6gR-BSZ9IuWyV7EgaQQayYBf_XaTW25DvL47T4tUhM_iVIC9Yonr_o56PSLyaDP-rYhmvqGiIdghqW-NDPkht04Ogooga-w3s1XEygo35XzKZ38c3E5STiA3x9NTtJKendkwuLUD4o2XjjIsVN0wUHMi5Xy-4kAkjmvHdf4v1GdMdtaauyP4K9G6MutkLWqIhUMi54MDhQr1ujk1sR8ZenYwHSPdZiYmyYLqGlBXZRzOUg8fvrQFWFeyRPFgvXJKuLGIAFbkW40Umo5oEEWkkpTAkvL54X5RqoXDI3tgF1VEd7jilYN1P2O5rzrlTKJ-rOQXAm3CmfAfTnM-2Skl1oL8KixFHhewdc523oIKDEKpFi8b-UoAoSc3k0Td3SoQABEZa1w1ukYGFp7q_b-ImNHcuPvOfRG7xYvLlzXAYYW_2LpJem0w-kAPOXDzg_hrvkfvQfP1Qqy5TvMMrZZ7LW2Qc-RB6tpC3fmqCjh-rhJjomrOou1VIUBdZis
{
    "DecodedMessage": "{\"allowed\":false,\"explicitDeny\":true,\"matchedStatements\":{\"items\":[{\"statementId\":\"\",\"effect\":\"DENY\",\"principals\":{\"items\":[{\"value\":\"AIDA2UC3F56EZO3SYA7Y7\"}]},\"principalGroups\":{\"items\":[]},\"actions\":{\"items\":[{\"value\":\"cloudtrail:LookupEvents\"},{\"value\":\"ec2:RequestSpotInstances\"},{\"value\":\"ec2:RunInstances\"},{\"value\":\"ec2:StartInstances\"},{\"value\":\"iam:AddUserToGroup\"},{\"value\":\"iam:AttachGroupPolicy\"},{\"value\":\"iam:AttachRolePolicy\"},{\"value\":\"iam:AttachUserPolicy\"},{\"value\":\"iam:ChangePassword\"},{\"value\":\"iam:CreateAccessKey\"},{\"value\":\"iam:CreateInstanceProfile\"},{\"value\":\"iam:CreateLoginProfile\"},{\"value\":\"iam:CreatePolicyVersion\"},{\"value\":\"iam:CreateRole\"},{\"value\":\"iam:CreateUser\"},{\"value\":\"iam:DetachUserPolicy\"},{\"value\":\"iam:PassRole\"},{\"value\":\"iam:PutGroupPolicy\"},{\"value\":\"iam:PutRolePolicy\"},{\"value\":\"iam:PutUserPermissionsBoundary\"},{\"value\":\"iam:PutUserPolicy\"},{\"value\":\"iam:SetDefaultPolicyVersion\"},{\"value\":\"iam:UpdateAccessKey\"},{\"value\":\"iam:UpdateAccountPasswordPolicy\"},{\"value\":\"iam:UpdateAssumeRolePolicy\"},{\"value\":\"iam:UpdateLoginProfile\"},{\"value\":\"iam:UpdateUser\"},{\"value\":\"lambda:AddLayerVersionPermission\"},{\"value\":\"lambda:AddPermission\"},{\"value\":\"lambda:CreateFunction\"},{\"value\":\"lambda:GetPolicy\"},{\"value\":\"lambda:ListTags\"},{\"value\":\"lambda:PutProvisionedConcurrencyConfig\"},{\"value\":\"lambda:TagResource\"},{\"value\":\"lambda:UntagResource\"},{\"value\":\"lambda:UpdateFunctionCode\"},{\"value\":\"lightsail:Create*\"},{\"value\":\"lightsail:Delete*\"},{\"value\":\"lightsail:DownloadDefaultKeyPair\"},{\"value\":\"lightsail:GetInstanceAccessDetails\"},{\"value\":\"lightsail:Start*\"},{\"value\":\"lightsail:Update*\"},{\"value\":\"organizations:CreateAccount\"},{\"value\":\"organizations:CreateOrganization\"},{\"value\":\"organizations:InviteAccountToOrganization\"},{\"value\":\"s3:DeleteBucket\"},{\"value\":\"s3:DeleteObject\"},{\"value\":\"s3:DeleteObjectVersion\"},{\"value\":\"s3:PutLifecycleConfiguration\"},{\"value\":\"s3:PutBucketAcl\"},{\"value\":\"s3:PutBucketOwnershipControls\"},{\"value\":\"s3:DeleteBucketPolicy\"},{\"value\":\"s3:ObjectOwnerOverrideToBucketOwner\"},{\"value\":\"s3:PutAccountPublicAccessBlock\"},{\"value\":\"s3:PutBucketPolicy\"},{\"value\":\"s3:ListAllMyBuckets\"},{\"value\":\"ec2:PurchaseReservedInstancesOffering\"},{\"value\":\"ec2:AcceptReservedInstancesExchangeQuote\"},{\"value\":\"ec2:CreateReservedInstancesListing\"},{\"value\":\"savingsplans:CreateSavingsPlan\"}]},\"resources\":{\"items\":[{\"value\":\"*\"}]},\"conditions\":{\"items\":[]}}]},\"failures\":{\"items\":[]},\"context\":{\"principal\":{\"id\":\"AIDA2UC3F56EZO3SYA7Y7\",\"name\":\"admin\",\"arn\":\"arn:aws:iam::730335670153:user/admin\"},\"action\":\"RunInstances\",\"resource\":\"arn:aws:ec2:us-east-1:730335670153:instance/*\",\"conditions\":{\"items\":[{\"key\":\"ec2:MetadataHttpPutResponseHopLimit\",\"values\":{\"items\":[{\"value\":\"1\"}]}},{\"key\":\"ec2:InstanceMarketType\",\"values\":{\"items\":[{\"value\":\"on-demand\"}]}},{\"key\":\"aws:Resource\",\"values\":{\"items\":[{\"value\":\"instance/*\"}]}},{\"key\":\"aws:Account\",\"values\":{\"items\":[{\"value\":\"730335670153\"}]}},{\"key\":\"ec2:AvailabilityZone\",\"values\":{\"items\":[{\"value\":\"us-east-1b\"}]}},{\"key\":\"ec2:ebsOptimized\",\"values\":{\"items\":[{\"value\":\"false\"}]}},{\"key\":\"ec2:IsLaunchTemplateResource\",\"values\":{\"items\":[{\"value\":\"false\"}]}},{\"key\":\"ec2:InstanceType\",\"values\":{\"items\":[{\"value\":\"t2.micro\"}]}},{\"key\":\"ec2:RootDeviceType\",\"values\":{\"items\":[{\"value\":\"ebs\"}]}},{\"key\":\"aws:Region\",\"values\":{\"items\":[{\"value\":\"us-east-1\"}]}},{\"key\":\"ec2:MetadataHttpEndpoint\",\"values\":{\"items\":[{\"value\":\"enabled\"}]}},{\"key\":\"ec2:InstanceMetadataTags\",\"values\":{\"items\":[{\"value\":\"disabled\"}]}},{\"key\":\"aws:Service\",\"values\":{\"items\":[{\"value\":\"ec2\"}]}},{\"key\":\"ec2:InstanceID\",\"values\":{\"items\":[{\"value\":\"*\"}]}},{\"key\":\"ec2:MetadataHttpTokens\",\"values\":{\"items\":[{\"value\":\"optional\"}]}},{\"key\":\"aws:Type\",\"values\":{\"items\":[{\"value\":\"instance\"}]}},{\"key\":\"ec2:Tenancy\",\"values\":{\"items\":[{\"value\":\"default\"}]}},{\"key\":\"ec2:Region\",\"values\":{\"items\":[{\"value\":\"us-east-1\"}]}},{\"key\":\"aws:ARN\",\"values\":{\"items\":[{\"value\":\"arn:aws:ec2:us-east-1:730335670153:instance/*\"}]}}]}}}"
}

```





