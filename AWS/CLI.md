

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

## AWS through bash
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

