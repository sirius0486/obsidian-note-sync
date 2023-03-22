## Access AWS

### 访问AWS
• To access AWS, you have three options:
	• **AWS Management Console (protected by password + MFA)** , 
		`AWS管理控制台` , 由密码 + MFA 保护
	• **AWS Command Line Interface (CLI):** protected by access keys, 
		 `AWS命令行界面` , 受访问密钥保护
	• **AWS Software Developer Kit (SDK)** - for code: protected by access keys
		`AWS软件开发者工具包` , 用于代码, 受访问密钥保护
• Access Keys are generated through the AWS Console
	`访问密钥(access keys)`是通过 `AWS控制台` 生成的
• Users manage their own access keys
	用户管理自己的 访问密钥`(access keys)`
• Access Key ID ~= username , Access Key ID 等同于 用户名
• Secret Access Key ~= password , Access Key 等同于 密码
• **Access Keys are secret, just like a password. Don’t share them** , 不要分享密钥

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
	- **Principal**: account/user/role to which this policy applied to
	- **Action**:  list of actions this policy allows or denies
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

### Password Policy
> 密码政策

- 强大的密码 = 为你的账户提供更高的安全性
- 在AWS中，你可以设置一个密码策略。
	- 设置一个最小的密码长度
	- 要求特定的字符类型。- 包括大写字母
		- 小写字母
		- 数字
		- 非字母数字字符
		- 允许所有IAM用户更改自己的密码
	- 要求用户在一段时间后改变他们的密码（密码到期）。
	- 防止密码重复使用

### MFA
> `Multi Factor Authentication` 多重因素验证

- 用户可以访问你的账户，并有可能改变配置或删除你的AWS账户中的资源
- 你想保护你的 `Root Accounts`(根用户)和 `IAM users`
- `MFA` = 你知道的密码 + 你拥有的安全设备
- `MFA`的主要好处: 如果密码被盗或被黑，账户就不会受到影响

> AWS 提供以下 MFA 设备选择

- Virtual MFA device
	- Google Authenticator (只能在移动设备上使用
	- )
	- Authy
- Universal 2nd Factor(U2F) Security Key
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)

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

