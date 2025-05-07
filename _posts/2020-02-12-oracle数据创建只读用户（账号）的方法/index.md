---
title: "Oracle创建只读用户（账号）的方法"
date: 2020-02-12
categories: 
  - "software_programming"
tags: 
  - "oracle"
---

第一步：创建用户（需要使用有dba管理员权限的用户创建一个新的用户，比如system） create user 用户名 identified by 密码 default tablespace 表空间;

第二步：赋连接权限 grant connect to 用户名; grant Resource to 用户名;

权限分类： DBA: 拥有全部特权，是系统最高权限，只有DBA才可以创建数据库结构。 RESOURCE:拥有Resource权限的用户只可以创建实体，不可以创建数据库结构。 CONNECT:拥有Connect权限的用户只可以登录Oracle，不可以创建实体，不可以创建数据库结构。 对于普通用户：授予connect, resource权限。 对于DBA管理用户：授予connect，resource, dba权限。

第三步：赋表权限（到表空间所属用户下执行） grant select on owner.表名 to 用户名;

如果有多表，可以用selece转换批量执行语句： select 'grant select on '||owner||'.'||object\_name||' to 用户名;' from dba\_objects where owner in ('owner') and object\_type='TABLE';

第四步：创建同义词： create or replace SYNONYM 用户名.表名 FOR owner.表名;

如果有多表，可以用selece转换批量执行语句： SELECT 'create or replace SYNONYM 用户名.'||object\_name||' FOR '||owner||'.'||object\_name||';' from dba\_objects where owner in ('owner') and object\_type='TABLE';

样例如下:

/\*\* 创建用户，system用户下执行\*\*/

create user NewUser\_TEST IDENTIFIED BY NewUser\_TEST default tablespace SD temporary tablespace TEMP profile DEFAULT;

grant connect to NewUser\_TEST; ---grant dba to NewUser\_TEST; grant resource to NewUser\_TEST; -- Grant/Revoke system privileges grant alter any procedure to NewUser\_TEST; grant create any procedure to NewUser\_TEST; grant create database link to NewUser\_TEST; grant debug any procedure to NewUser\_TEST; grant debug connect session to NewUser\_TEST; grant unlimited tablespace to NewUser\_TEST; grant Create any synonym to NewUser\_TEST; grant create any view to NewUser\_TEST;

/\*\* 为用户赋权，老用户下执行 \*\*/ GRANT SELECT ON XXX.TB\_PARA\_CURRENCY TO NewUser\_TEST;

/\*\* 创建同义词，新用户下执行 \*\*/ create or replace synonym 表名 for 老用户.TB\_XXX;
