# basics

From a shell prompt:
```
aws s3 cp basics.md s3://data-space
aws s3 ls s3://data-space
```

EC2 - http://docs.aws.amazon.com/cli/latest/userguide/cli-using-ec2.html
```
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
chmod 400 MyKeyPair.pem
```

```
aws ec2 create-security-group --group-name my-sg --description "My security group"
```
Replace `sg-79939702` in the following command with the value you find in the `GroupId` field of the output from the previous command.
Replace `141.133.86.47` with the value returned by http://checkip.amazonaws.com (assuming your browser is on the same computer as your shell).
```
aws ec2 authorize-security-group-ingress --group-id sg-79939702 --protocol tcp --port 22 --cidr 141.133.86.47/24
```


Get the AMI-id from the Launch Instance page of AWS. 
Note that `t1.micro` doesn't work with some AMIs 
```
aws ec2 run-instances --image-id ami-cbdd50dc --count 1 --instance-type t2.nano --key-name MyKeyPair --security-groups my-sg
```
