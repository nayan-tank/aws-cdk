# aws-cdk
AWS Cloud Development Kit (AWS CDK)

AWS CDK (Cloud Development Kit) is an open-source software development framework to define cloud infrastructure in code and provision it through AWS CloudFormation.
Instead of writing YAML or JSON (like in raw CloudFormation), you write infrastructure code using real programming languages like:

- TypeScript
- Python
- Java
- C#/.NET
- Go

# Example: Create an S3 Bucket using Python AWS CDK
### Step 1: Install CDK
`npm install -g aws-cdk`

### Step 2: Create CDK Project
```
cdk init app --language python
```

### Step 3: Install Dependencies
```
source .venv/bin/activate
pip install aws-cdk.aws-s3
```

### Step 4: Edit my_cdk_stack.py
```
from aws_cdk import (
    Stack,
    aws_s3 as s3,
)
from constructs import Construct

class MyCdkStack(Stack):

def __init__(self, scope: Construct, construct_id: str, **kwargs) -> None:
    super().__init__(scope, construct_id, **kwargs)
    # Create S3 Bucket
    s3.Bucket(self, "MyFirstBucket",
        versioned=True,
        public_read_access=False
    )
```
### Step 5: Deploy
```
cdk synth     # Shows generated CloudFormation
cdk deploy    # Provisions resources
```



## Real-World Example: Lambda + API Gateway
In Python CDK, you'd write code that creates:

- An AWS Lambda function
- An API Gateway that triggers the Lambda

```
from aws_cdk import (
    aws_lambda as _lambda,
    aws_apigateway as apigw,
    Stack
)
from constructs import Construct

class MyCdkStack(Stack):
    def __init__(self, scope: Construct, id: str, **kwargs):
        super().__init__(scope, id, **kwargs)

        fn = _lambda.Function(
            self, "MyFunction",
            runtime=_lambda.Runtime.PYTHON_3_8,
            handler="index.handler",
            code=_lambda.Code.from_asset("lambda")
        )

        apigw.LambdaRestApi(
            self, "MyAPI",
            handler=fn
        )
```

# When to Use AWS CDK?
- You're already comfortable with programming languages.
- You want to reuse, test, and scale your infrastructure logic.
- You want better maintainability and modularity than raw CloudFormation.
