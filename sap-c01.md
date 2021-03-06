---
title: "AWS SAA-C02:知识体系+401题解析"
author: "hjpotter"
cover: "/img/saa.png"
tags: ["aws", "saa-c02"]
date: 2020-11-01T01:42:34+09:00


---

近日考完AWS SAA-C02（ AWS Certified Solutions Architect - Associate）认证。分享一下参考题目以及部分题目的解法分析。希望能帮助到正在准备考试的朋友们。

<!--more-->

##### 1

A company runs a legacy system on a single m4.2xlarge Amazon EC2 instance with Amazon EBS2 storage. The EC2 instance runs both the web server and a self-managed Oracle database. A snapshot is made of the EBS volume every 12 hours, and an AMI was created from the fully configured EC2 instance.
A recent event that terminated the EC2 instance led to several hours of downtime. The application was successfully launched from the AMI, but the age of the
EBS snapshot and the repair of the database resulted in the loss of 8 hours of data. The system was also down for 4 hours while the Systems Operators manually performed these processes.
What architectural changes will minimize downtime and reduce the chance of lost data?

- A. Create an Amazon CloudWatch alarm to automatically recover the instance. Create a script that will check and repair the database upon reboot. Subscribe the Operations team to the Amazon SNS message generated by the CloudWatch alarm.

- B. Run the application on m4.xlarge EC2 instances behind an Elastic Load Balancer/Application Load Balancer. Run the EC2 instances in an Auto Scaling group across multiple Availability Zones with a minimum instance count of two. Migrate the database to an Amazon RDS Oracle Multi-AZ DB instance.

- C. Run the application on m4.2xlarge EC2 instances behind an Elastic Load Balancer/Application Load Balancer. Run the EC2 instances in an Auto Scaling group across multiple Availability Zones with a minimum instance count of one. Migrate the database to an Amazon RDS Oracle Multi-AZ DB instance.

- D. Increase the web server instance count to two m4.xlarge instances and use Amazon Route 53 round-robin load balancing to spread the load. Enable Route 53 health checks on the web servers. Migrate the database to an Amazon RDS Oracle Multi-AZ DB instance.

  

一家公司在具有Amazon EBS2存储的单个m4.2xlarge Amazon EC2实例上运行遗留系统。 EC2实例同时运行Web服务器和自管理的Oracle数据库。每12小时对EBS卷进行一次快照，并从完全配置的EC2实例创建AMI。
最近终止EC2实例的事件导致数小时的停机时间。该应用程序是从AMI成功启动的，但是
EBS快照和数据库修复导致丢失8个小时的数据。在系统操作员手动执行这些过程的同时，系统也停机了4个小时。
哪些体系结构更改将最大程度地减少停机时间并减少丢失数据的机会？

-A.创建一个Amazon CloudWatch警报以自动恢复实例。创建一个脚本，该脚本将在重新启动后检查并修复数据库。将Operations团队订阅到CloudWatch警报生成的Amazon SNS消息。
-B.在Elastic Load Balancer / Application Load Balancer之后的m4.xlarge EC2实例上运行应用程序。跨多个可用区在Auto Scaling组中运行EC2实例，实例数量最少为2。将数据库迁移到Amazon RDS Oracle Multi-AZ数据库实例。
-C.在Elastic Load Balancer / Application Load Balancer之后的m4.2xlarge EC2实例上运行应用程序。跨多个可用区在Auto Scaling组中运行EC2实例，最小实例数为1。将数据库迁移到Amazon RDS Oracle Multi-AZ数据库实例。
-D.将Web服务器实例数增加到两个m4.xlarge实例，并使用Amazon Route 53循环负载均衡来分散负载。在Web服务器上启用Route 53健康检查。将数据库迁移到Amazon RDS Oracle Multi-AZ数据库实例。

B There are 2 problems here. Firstly, the EBS snapshot is too old and secondly, the outage resulted in DB issues and data loss. Using 2 instances installed with the web server and using Route 53 load balancing should help with the first problem and RDS Multi-AZ DB would help in the second. A: This will not reduce the chances of lost data and downtime could still be significant and risky. B\D: I chose this simply because of the LB\Auto Scaling. While Route 53 can do similar function, it does not auto heal the instance to bring it back to healthy state. C: There is only 1 active instance, there should be at least 2.

这里有两个问题。 首先，EBS快照太旧，其次，中断导致数据库问题和数据丢失。 使用Web服务器上安装的2个实例以及使用Route 53负载平衡应该可以解决第一个问题，而使用RDS Multi-AZ DB可以解决第二个问题。 答：这不会减少丢失数据的机会，停机时间仍然可能是巨大且危险的。 B \ D：我之所以选择它仅仅是因为LB \ Auto Scaling。 虽然Route 53可以执行类似的功能，但它不会自动修复实例以使其恢复健康状态。 C：只有1个活动实例，至少应有2个。

##### 2

A Solutions Architect is working with a company that operates a standard three-tier web application in AWS. The web and application tiers run on Amazon EC2 and the database tier runs on Amazon RDS. The company is redesigning the web and application tiers to use Amazon API Gateway and AWS Lambda, and the company intends to deploy the new application within 6 months. The IT Manager has asked the Solutions Architect to reduce costs in the interim.
Which solution will be MOST cost effective while maintaining reliability?

- A. Use Spot Instances for the web tier, On-Demand Instances for the application tier, and Reserved Instances for the database tier.
- B. Use On-Demand Instances for the web and application tiers, and Reserved Instances for the database tier.
- C. Use Spot Instances for the web and application tiers, and Reserved Instances for the database tier.
- D. Use Reserved Instances for the web, application, and database tiers.

解决方案架构师正在与一家在AWS中运行标准三层Web应用程序的公司合作。 Web和应用程序层在Amazon EC2上运行，数据库层在Amazon RDS上运行。 该公司正在重新设计Web和应用程序层以使用Amazon API Gateway和AWS Lambda，并且该公司计划在6个月内部署新应用程序。 IT经理已要求解决方案架构师在此期间降低成本。
哪种解决方案在保持可靠性的同时最具成本效益？

A.将竞价型实例用于Web层，将按需实例用于应用程序层，并将预留实例用于数据库层。
B.将按需实例用于Web和应用程序层，并将保留实例用于数据库层。
C.将竞价型实例用于Web和应用程序层，将预留实例用于数据库层。
D.对Web，应用程序和数据库层使用保留实例。

