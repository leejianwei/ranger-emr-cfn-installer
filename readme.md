# Cloudformation Templates for Ranger Self Installing and Integrating with AWS EMR Cluster and AD/LDAP

---

Author：Laurence Geng　　｜　　Created Date：2020-11-21　　｜　　Updated Date：2020-11-21

---

This project is a series of aws cloudformation templates which are used to install ranger and integrate a AWS EMR cluster and a windows AD or Open LDAP server as authentication channel. There is another closely related project: **[ranger-emr-cli-installer](https://github.com/bluishglc/ranger-emr-cli-installer)** which does the same job via command line. The two projects are very close, but can work independently，you can pick anyone as you wish.

## 1. Ranger Introduction

Let’s check out Ranger's architecture:

![ranger-architecture](https://user-images.githubusercontent.com/5539582/99872048-f0c24480-2c19-11eb-8c0f-43df2552837c.png)

Ranger has 5 parts:

1. Ranger Admin Service
2. Ranger UserSync Service
3. A Backend RDB for Storing User's Authorization
4. A Solr Server for Storing Audit Log
5. A Series of Plugins for Big Data Components/Services

Besides above, there are 2 external dependencies For Ranger to integrate:

6. A Windows AD or Open LDAD Server as Authentication Channel
7. A Hadoop (AWS EMR) Cluster to Be Managed by Ranger

So, a fully Ranger installation will cover following jobs:

1. Install JDK (Required by Ranger Admin and Solr)
2. Install MySQL (As Ranger Backend RDB)
3. Install Solr (As Ranger Audit Store)
4. Install Ranger Admin (and Integrate with AD/LDAP Server)
5. Install Ranger UserSync (and Integrate with AD/LDAP Server)
6. Install Ranger Plugins (i.e. HDFS, Hive, HBase and so on)

## 2. Cloud Formation Templates Introduction

There are 4 templates files in projects, here is difference:

Template Files|Integrated Authentication Service|AWS Region
--------------|---------------------------------|----------
ranger-emr-ad.template|Windows AD|Global Regions
ranger-emr-ad.cn.template|Windows AD|China Regions
ranger-emr-ldap.template|Open LDAP|Global Regions
ranger-emr-ldap.cn.template|Open LDAP|China Regions

## 3. Usage Examples

To explain how to use this tool, assume we have following environment:

**A Windows AD Server:**

Info Item Key|Info Item Value
---------|-----
IP|10.0.0.194
Domain Name|corp.emr.local
Base DN|cn=users,dc=corp,dc=emr,dc=local
Bind DN|cn=ranger,ou=service accounts,dc=example,dc=com
Bind DN Password|Admin1234!
User Object Class|person

**An Open LDAP Server:**

Info Item Key|Info Item Value
---------|-----
IP|10.0.0.41
Base DN|dc=example,dc=com
Bind DN|cn=ranger,ou=service accounts,dc=example,dc=com
Bind DN Password|Admin1234!
User DN Pattern|uid={0},dc=example,dc=com
Bind Group Search Filter|(member=uid={0},dc=example,dc=com)
User Object Class|inetOrgPerson


**A Multi-Master EMR Cluster:**

Node|IP
---|---
Master Nodes|10.0.0.177,10.0.0.199,10.0.0.21
Core Nodes|10.0.0.114,10.0.0.136


**A Normal EMR Cluster:**

Node|IP
---|---
Master Nodes|10.0.0.177,10.0.0.199,10.0.0.21
Core Nodes|10.0.0.114,10.0.0.136

### 4.1. Install Ranger + Integrate a Window AD Server + Integrate A Multi-Master EMR Cluster

TBD

### 4.2. Install Ranger + Integrate a Open LDAP Server + Integrate A Multi-Master EMR Cluster

TBD



