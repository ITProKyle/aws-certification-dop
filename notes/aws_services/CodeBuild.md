# [CodeBuild](https://console.aws.amazon.com/codesuite/codebuild/start)

- it's an on demand service
  - only pay for minutes run
- fully managed build service
  - compile code
  - run tests
  - produce artifacts
  - deploy artifacts (where [CodeDeploy](./CodeDeploy.md) or other services are not better suited)
- eliminates the need to provision/manage/scale a build server
  - scales automatically
- provides pre-packaged build environments
  - linux only (at the time of writing)
- allows for custom build environments (docker image)
- can be deployed in a vpc
- configured with [buildspec.yml](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

## Links & Additional Resources

- [CloudFormation Resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_CodeBuild.html)
- [Actions, Resources, and Condition Keys for AWS CodeBuild](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awscodebuild.html)
- [User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html)
