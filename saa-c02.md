aws

![image-20200703165311152](/Users/gaoyunhu/Library/Application Support/typora-user-images/image-20200703165311152.png)



#### 1

```b c
A solutions architect is designing a new service behind Amazon API Gateway.
The request patterns for the service will be unpredictable and can change suddenly from 0
requests to over 500 per second.
The total size of the data that needs to be persisted in a backend database is currently less than
1 GB with unpredictable future growth Data can be queried using simple key-value requests.
Which combination of AWS services would meet these requirements? (Select TWO )
前需要保留在后端数据库中的数据总大小小于
1 GB，未来增长不可预测。可以使用简单的键值请求查询数据。
哪种AWS服务组合可以满足这些要求？ （选择两个）
A. AWS Fargate
B. AWS Lambda
C. Amazon DynamoDB
D. Amazon EC2 Auto Scaling
E. MySQL-compatible Amazon Aurora
bc
```

QUESTION 2
```
A solutions architect needs to design a managed storage solution for a company's application
that includes high-performance machine learning,
This application runs on AWS Fargate and the connected storage needs to have concurrent
access to files and deliver high performance.
Which storage option should the solutions architect recommend?
A. Create an Amazon S3 bucket for the application and establish an IAM role for Fargate to
communicate with Amazon S3.
B. Create an Amazon FSx for Lustre file share and establish an IAM role that allows Fargate to
communicate with FSx for Lustre.
. Create an Amazon Elastic File System (Amazon EFS) file share and establish an IAM role that
allows Fargate to communicate with Amazon EFS.
D. Create an Amazon Elastic Block Store (Amazon EBS) volume for the application and establish an
IAM role that allows Fargate to communicate with Amazon EBS.
Answer: B
```
Explanation:
https://aws.amazon.com/efs/
Keyword: Concurrent Access to files + Deliver High Performance
Amazon FSx .



4

QUESTION 4

```xml
A company runs an internal browser-based application The application runs on Amazon EC2
instances behind an Application Load Balancer.
The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones.
The Auto Scaling group scales up to 20 instances during work hours, but scales down to 2
instances overnight Staff are complaining that the application is very slow when the day begins,
although it runs well by mid-morning,
How should the scaling be changed to address the staff complaints and keep costs to a
minimum?
A. Implement a scheduled action that sets the desired capacity to 20 shortly before the office opens
B. Implement a step scaling action triggered at a lower CPU threshold, and decrease the cooldown
period
C. Implement a target tracking action triggered at a lower CPU threshold and decrease the cooldown
period
D.
Implement a scheduled action that sets the minimum and maximum capacity to 20 shortly before
the office opens
Answer: C
```

公司运行基于内部浏览器的应用程序。该应用程序在Application Load Balancer后面的Amazon EC2实例上运行。实例在多个可用区中的Amazon EC2 Auto Scaling组中运行。 Auto Scaling小组在工作时间内最多可扩展20个实例，但在一夜之间最多可扩展到2个实例员工抱怨说，一天开始时应用程序运行非常缓慢，尽管它在上午中旬运行良好，但如何将扩展比例更改为解决员工的投诉并使费用降到最低？

A.实施计划的行动，以在办公室开放之前不久将所需容量设置为20。B.实施以较低的CPU阈值触发的逐步扩展操作，并减少冷却时间C.实施以较低的CPU阈值触发的目标跟踪操作并缩短冷却时间D。实施计划的行动，在办公室开业前不久将最小和最大容量设置为203ryou
