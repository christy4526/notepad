# CentOS 7.x MySQL 5.7 설치

참고링크  
- https://cherrypick.co.kr/how-to-install-mysql5-7-in-centos7/  
- https://mosei.tistory.com/entry/MySQL-57-세팅-CentOS7  

### wget 설치
```
$ yum install wget
```

### MySQL 다운로드
```
$ wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
``` 

### MySQL 설치
```
$ sudo rpm -ivh mysql57-community-release-el7-11.noarch.rpm
```
 
### MySQL 서버 설치
```
$ sudo yum install mysql-server
```
 
### 서비스 시작
```
$ sudo systemctl start mysqld
``` 

### 보안 스크립트 실행  
MySQL은 루트 로그인이나 샘플 유저와 같이 보안 수준이 낮은 기본 옵션을 변경해주는 보안 스크립트가 포함 되어있다.  
```
$ sudo mysql_secure_installation  
  
# 실행결과
The existing password for the user account root has expired. Please set a new password.

New password:
```

## 비밀번호 재설정
### MySQL 정지
```
$ systemctl stop mysqld
```
 
### MySQL 환경 옵션 설정
```
$ systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"
```

### MySQL 시작
```
$ systemctl start mysqld
```
 
### MySQL 로그인
루트의 비밀번호 없이 로그인 가능
```
$ mysql -u root
```
 
### 루트 비밀번호 변경
5.7부터 비밀번호 컬럼이 password에서 authentication_string으로 변경됐다.
```
mysql> UPDATE mysql.user SET authentication_string = PASSWORD('새로운 비밀번호')
    -> WHERE User = 'root' AND Host = 'localhost';
mysql> FLUSH PRIVILEGES;
mysql> exit
```
 
### MySQL 정지
```
$ systemctl stop mysqld
```
 
### MySQL 환경 옵션 설정 해제
다음 접속부터는 정상적으로 로그인할 수 있도록 환경 옵션 설정 해제를 한다.
```
$ systemctl unset-environment MYSQLD_OPTS
```

### MySQL 시작
```
$ systemctl start mysqld
```
 
### 사용자 추가
```
mysql> create user '사용자'@'localhost' identified by '비밀번호';
```
 
### 권한 부여
```
mysql> grant all privileges on *.* to '사용자'@'%';
```
 
### 외부 접속 허용
외부의 MySQL 워크벤치와 같은 툴에서 접속을 가능하게 하기 위해서 아래의 설정을 추가한다.
```
$ vi /etc/my.cnf
bind-address 0.0.0.0 # 없으면 추가해준다.
```


### 외부 접속 허용(firewall)
```
# yum install firewalld

# systemctl start firewalld

# systemctl enable firewalld

(서비스 재구동시에는 #firewall-cmd --reload 명령 사용)

//public은 zone 이름이며, 클라우드 시스템처럼 zone 형태로 방화벽 포트들을 관리할수 있음

# firewall-cmd  --permanent  --zone=public --add-port=3306/tcp

//포트를 범위로 지정하기

# firewall-cmd --permanent --zone=public --add-port=5000-5100/tcp

//포트 삭제

# firewall-cmd --permanent --zone=public --remove-port=3306/tcp

//모든 접속을 허용하고 싶을때 (방화벽을 내리지 않고, zone을 trusted로 변경)

# firewall-cmd --set-default-zone=trusted
```
