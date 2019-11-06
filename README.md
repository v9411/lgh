# Node-MySQL sample for Kubernetes

쿠버네티스를 위한 샘플입니다.

node 와 mysql 을 사용한 게시판입니다.

[https://github.com/achowba/node-mysql-crud-app](https://github.com/achowba/node-mysql-crud-app)를 수정했습니다.


## MySQL 설정
~~~
CREATE USER 'test'@'%' IDENTIFIED WITH mysql_native_password BY 'Welcome1';

GRANT USAGE ON *.* TO 'test'@'%';

GRANT ALL PRIVILEGES ON *.* TO 'test'@'%';

CREATE DATABASE sample DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

USE sample;

CREATE TABLE IF NOT EXISTS `players` (
  `id` int(5) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(255) NOT NULL,
  `last_name` varchar(255) NOT NULL,
  `position` varchar(255) NOT NULL,
  `number` int(11) NOT NULL,
  `user_name` varchar(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  AUTO_INCREMENT=1;
~~~


## 환경설정
~~~
export MYSQL_SERVICE_HOST={MYSQL_IP}
export MYSQL_SERVICE_USER=test
export MYSQL_SERVICE_PASSWORD=Welcome1
export MYSQL_SERVICE_DATABASE=sample
~~~

## 실행
~~~
$ npm install
$ npm start
~~~

## Docker 이미지 생성
~~~
docker build -t sample-app .
~~~

## Docker 실행
~~~
docker run --name app  -e MYSQL_SERVICE_HOST={MYSQL_IP} -e MYSQL_SERVICE_USER=test -e MYSQL_SERVICE_PASSWORD=Welcome1 -e MYSQL_SERVICE_DATABASE=sample  -p 8080:8080 -it sample-app
~~~