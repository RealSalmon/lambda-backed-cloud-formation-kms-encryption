## Using AWS KMS to Encrypt Values in CloudFormation Stacks

This repository contains an AWS Lambda-backed custom resource for AWS
CloudFormation. The custom resource will encrypt values using AWS Key
Management Service (KMS) and make the ecrypted version available to the
template.

The included example CloudFormation template
(lambda-backed-cloud-formation-kms-encryption.template) demonstrates the
usage of the custom resource.

For additional information, please read the in-depth article on 
implementing this custom resource at 
[https://ben.fogbutter.com/2016/02/22/using-kms-to-encrypt-cloud-formation-values.html]
(https://ben.fogbutter.com/2016/02/22/using-kms-to-encrypt-cloud-formation-values.html)

### Syntax

```json
{
    "Type": "AWS::CloudFormation::CustomResource",
    "Version": "1.0",
    "Properties": {
      "ServiceToken": String,
      "KeyId": String,
      "PlainText": String
    }
  }
}
```

### Properties

#### ServiceToken
The ARN of the AWS Lambda function backing the custom resource.

#### PlainText
The plain text value that should be encrypted.

#### KeyId
The key ID of the AWS KMS key that should be used to encrypt the value
provided in PlainText. Note that the Lambda function backing this
custom resource must have encrypt permissions for the specified key.


### Return Values

#### Ref

When you provide the custom resource's logical name to the Ref intrinsic
function, a GUID will be returned. This value has no meaning whatsoever,
and is only supplied because CloudFormation requires a value.

For more information about using the Ref function, see [Ref]
(http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html).

#### Fn::GetAtt

Fn::GetAtt returns a value for a specified attribute of this type. This
section lists the available attributes and sample return values.

- **CipherText**: The Base64 encoded, encrypted format of the value that
                  was supplied for the PlainText property.

For more information about using Fn::GetAtt, see [Fn::GetAtt]
(http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html).
  