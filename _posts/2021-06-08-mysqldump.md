---
layout: post
title: "[20210608] Database의 테이블 구조와 데이터 옮기기 using mysqldump"
date: 2021-06-08 22:36
last_modified_at: 2021-06-08 22:36
tags: [mysql]
toc: true
---

Local database에 있는 table 구조와 data를 AWS RDS로 옮기기 위해서 mysqldump를 사용하였다.
mysql에서는 migration을 위해서 mysqldump라는 툴을 제공해주었고, Local DB와 AWS RDS의 데이터베이스가 각각 MySQL, MariaDB여서 쉽게 할 수 있었다.  
하지만, 다른 곳에서 문제가 발생해서 시간이 많이 걸렸는데 문제가 되었던 부분은 Character set이랑 Collation이었다.  
MySQL에서는 지원하는 인스턴스들이 MariaDB에서는 지원하지 않았던 것이다.  
DB version이 mysql은 8.0.18이었고, AWS RDS는 MariaDB 10.4.13이었기 때문에 서로 호환성이 되지 않는 부분이 발생하면서 생기는 문제였다.
그래서 해당 설정 값들을 모두 MariaDB에서 지원하는 값으로 변경하느라 애먹었다. database, table, 심지어 column까지 하나하나 다 설정 되어있었다.
이를 모두 변경하고 나니 mysqldump가 제대로 동작하였다.
사실 이것도 확인만 잘 했다면 시간이 오래걸릴만한 문제는 아니었던것 같다...

---

### 출처

mysqldump 출처 : https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.SmallExisting.html
