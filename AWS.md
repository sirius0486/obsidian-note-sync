## IAM : Users & Groups
• **IAM** = Identity and Access Management, Global service  
• **Root account** created by default, shouldn’t be used or shared  
• **Users** are people within your organization, and can be grouped  
• **Groups** only contain users, not other groups  
• Users don’t have to belong to a group, and user can belong to multiple groups

### Permissions
用户或组可以被分配称为策略 (`policies`) 的 `JSON` 文件
1. 这些策略定义了用户的权限(`permissions`)
2. 在AWS中，你要应用最小权限原则：不要给用户超过需要的权限

```json
{
  "Version": "2012-10-17", 
  "Statement": [
    {
      "Effect": "Allow", 
      "Action": "ec2:Describe*",
      "Resource": "*"
    }, 
    {
      "Effect": "Allow",
      "Action": "elasticloadbalancing:Describe*", 
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
            "cloudwatch:ListMetrics", 
            "cloudwatch:GetMetricStatistics", 
            "cloudwatch:Describe*"
      ],
      "Resource": "*"
   }
  ]
}
```

### Policies inheritance
> 权限继承
![[Pasted image 20230322112640.png]]


### Policies Structure

- **Version** :  `policy language version` , 政策语言版本
- **Id** :  `Policies` 政策的标识符
- **Statement**: `声明`
	- **Sid**:  `Statement` 的标识符 (可选)
	- **Effect** : `Statement` 是否可以被 访问( Allow, Deny)
	- **Principal**:  -   account/user/role towhichthispolicyappliedto
	- **Action**: 
	- **Resource**: `Action` 使用的资源清单
	- **Condition** : 该政策无效时的条件（可选）

```json
{
  "Version": "2012-10-17", 
  "Id": "S3-Account-Permissions",
  "Statement": [
    {
      "Sid": "1", 
      "Effect": "Allow",
      "Principal": {
        "AWS": ["arn:aws:iam::123456789012:root"]
      },
      "Action":[
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource":["arn:aws:s3:::mybucket/*"]
    }
  ]
}
```


## Dynamo DB

- partition key
- sort key

![[Pasted image 20230322093637.png]]

```ts
import * as AWS from 'aws-sdk';

AWS.config.update({
  region: 'your-region',
  accessKeyId: 'your-access-key-id',
  secretAccessKey: 'your-secret-access-key'
});

const docClient = new AWS.DynamoDB.DocumentClient();

const params = {
  TableName: 'your-table-name',
  Item: {
    id: 1,
    name: 'Alice',
    email: 'alice@example.com',
    age: 25
  }
};

docClient.put(params, (err, data) => {
  if (err) {
    console.error('Unable to add item. Error JSON:', JSON.stringify(err, null, 2));
  } else {
    console.log('Added item:', JSON.stringify(data, null, 2));
  }
});
```


## Lambda


## S3

