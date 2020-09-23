# Install requirements
### Install python
```
# python 버전과 Django버전이 같아야함.  
# python은 gcc 필요  
sudo yum install gcc openssl-devel bzip2-devel libffi-devel  
  
# Download Python3.7  
cd /usr/src  
sudo wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz  
  
sudo tar xzf Python-3.7.3.tgz  
  
# Install Python3.7 
cd Python-3.7.3  
sudo ./configure --enable-optimizations  
sudo make altinstall  
  
# Edit bashrc  
# 1. python3 -V : 3.7.3  
sudo ln -s /usr/local/bin/python3.7 /bin/python3  

# 2. python -V : 3.7.3  
sudo ls -l /bin/python*  
sudo unlink /bin/python  
sodu ln -s /usr/local/bin/python3.7 /bin/python  
```
참고 : https://hello-bryan.tistory.com/135
  
  
### Install pip
```
yum install python-pip
```
  
### Install Django 
```
pip install django  
```
  
### Django 설치 확인 & 프로젝트 생성
```
django-admin startproject testproject
```
  
### Run server
```
# manage.py가 있는 폴더 경로에서 실행 
python manage.py runserver
# python manage.py runserver 0:8000  
  
# 백그라운드에서 실행하는 방법  
# https://znznzn.tistory.com/23?category=819327  
python manage.py runserver 0.0.0.0:8000 &  
python manage.py runserver 0:8000 &  
```
  
### 외부 접속 허용
```
# 1. django "setting.py" 파일의 옵션 설정  
ALLOWED_HOSTS = '*'  
  
2. 사용하고자 하는 포트 관련 외부 방화벽 열어주기

# ufw allow 8000/tcp
```
  

참고 : https://znznzn.tistory.com/42
