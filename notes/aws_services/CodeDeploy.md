# [CodeDeploy](https://console.aws.amazon.com/codesuite/codedeploy/start)

- fully managed deployment service that automated deployment to:
  - ec2 instances (auto-scaling groups & standalone)
  - on-prem systems
  - [lambda functions](https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-lambda-sam.html)
- makes it easier to:
  - rapidly deploy new features
  - update lambda function versions
  - avoid downtime during deployment
  - handle complex automated deployment process
- configured with [appspec.yml](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html)

## EC2 Instances

### Example [appspec.yml](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html)

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html/WordPress
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root
  AfterInstall:
    - location: scripts/change_permissions.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
    - location: scripts/create_test_db.sh
      timeout: 300
      runas: root
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 300
      runas: root
```

### Example userdata.txt

```bash
#!/bin/bash
sudo apt-get update -y
sudo apt-get install ruby -y
sudo apt-get install wget -y
cd /home/ubuntu
wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
service codedeploy-agent start
rm install
```

## Links & Additional Resources

- [CloudFormation Resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_CodeDeploy.html)
- [Actions, Resources, and Condition Keys for AWS CodeDeploy](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awscodedeploy.html)
- [User Guide](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html)
