
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

### Example Access Keys
> 这是一个虚假的密钥, 仅做参考

![[Pasted image 20230322130636.png]]
### AWS CLI
> 它是开源的 https://github.com/aws/aws-cli

- `AWS CLI` 是一个使你能够使用命令行的命令与 `AWS服务` 互动的工具
- 直接访问 AWS服务 的 公共API
- 你可以开发脚本来管理你的资源
- 使用`AWS管理控制台`的替代方案

### AWS SDK
> AWS Software Development Kit  `AWS软件开发工具包`

- 特定语言的API(一组库)
- 使你能够以编程方式访问和管理AWS服务
- 嵌入您的应用程序中
- 支持
	- SDK（JavaScript、Python、PHP、.NET、Ruby、Java、Go、Node.js、C++）
	- 移动SDK（Android，iOS，...）
	- 物联网设备SDK（嵌入式C，Arduino，...)
- `AWS CLI`是建立在`AWS SDK for Python`之上的。
![[Pasted image 20230322131352.png]]
### IAM Roles for Services
• Some AWS service will need to perform actions on your behalf
• To do so, we will assign permissions to AWS services with IAM Roles
• Common roles:
	• EC2 Instance Roles
	• Lambda Function Roles
	• Roles for CloudFormation

![[Pasted image 20230322131621.png]]
### IAM Security Tools

• **IAM Credentials Report (account-level)**  
	• a report that lists all your account's users and the status of their various credentials

• **IAM Access Advisor (user-level)**  
	• Access advisor shows the service permissions granted to a user and when those services were last accessed.  
	• You can use this information to revise your policies.

### IAM指南和最佳实践
- 除了设置AWS账户，不要使用根账户 
-  一个物理用户 = 一个AWS用户
- 将用户分配给组，并将权限分配给组
- 创建一个强大的密码策略
- 使用并强制使用**多因素认证（MFA）**
- 创建和使用角色，为AWS服务赋予权限
- 使用访问密钥进行程序化访问（CLI / SDK）
- 使用IAM凭证报告审核您的账户权限 
- **不要共享IAM用户和访问密钥**

### IAM Section – Summary
- 用户(Users)：映射到一个物理用户，有AWS控制台的密码
- 组(Groups)：只包含用户
- 策略(Policies)。JSON文档，概述了用户或组的权限 
- 角色(Roles)：用于EC2实例或AWS服务
- 安全性(Security)。MFA + 密码策略
- 访问密钥(Access Keys)：使用CLI或SDK访问AWS
- 审计(Audit)。IAM凭证报告和IAM访问顾问


## EC2
• EC2 is one of the most popular of AWS’ offering
	`EC2 是AWS最受欢迎的产品之一`
• EC2 = Elastic Compute Cloud = Infrastructure as a Service
	`EC2 = 弹性计算云 = 基础设施即服务`
• It mainly consists in the capability of :  主要包括以下功能:
	• Renting virtual machines (EC2)  `租用虚拟机（EC2）`
	• Storing data on virtual drives (EBS)  `在虚拟驱动器上存储数据（EBS)`
	• Distributing load across machines (ELB) `在机器之间分配负载（ELB）`
	• Scaling the services using an auto-scaling group (ASG) `使用自动扩展组（ASG）扩展服务`
	
• Knowing EC2 is fundamental to understand how the Cloud works `了解EC2是了解云计算工作的基础`

### EC2 sizing & configuration options

- 操作系统（OS）: `Linux`、`Windows或` `Mac OS `
- 多少计算能力和核心（CPU）
- 多少随机存取内存(RAM)
- 多少存储空间。
	- 网络连接的（EBS和EFS） 
	- 硬件（EC2实例库）
- 网卡：网卡的速度，公共IP地址
- 防火墙规则：安全组
- 启动脚本（首次启动时配置）: EC2用户数据

### EC2 User Data
- 可以使用`EC2 User data Script` (用户数据脚本)来引导(bootstrap)我们的实例(instances)
- 引导意味着在机器启动时启动命令
- 该脚本只在实例**首次启动时**运行一次
- EC2用户数据用于自动启动任务，如
	- 安装更新
	- 安装软件
	- 从互联网上下载普通文件
	- 任何你能想到的事情
- EC2用户数据脚本以根用户的身份运行

### Security Groups
- 安全组是AWS中网络安全的基础
- 他们控制流量如何被允许进入或离开我们的EC2实例
- 安全组只包含规则
- 安全组规则可以通过IP或安全组来引用

> 安全组在EC2实例上扮演着 "防火墙 "的角色
- 它们负责
	- 对端口的访问
	- 授权的IP范围 - IPv4和IPv6
	- 对入站网络的控制（从其他地方到实例）。
	- 控制出站网络（从实例到其他）


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

