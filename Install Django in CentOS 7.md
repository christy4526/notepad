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



참고 : https://znznzn.tistory.com/42
