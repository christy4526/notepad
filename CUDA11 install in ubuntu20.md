## 1. gcc를 준비  
CUDA 10.1을  설치하려면 gcc 8을 사용해야 하지만 GPU 드라이버를 설치하기 위해 gcc 9가 필요  
Ubuntu 20.04의 디폴트 gcc 버전이 9이기 때문에 build-essential 패키지 설치시 gcc 9가 같이 설치됨  
```
sudo apt update
sudo apt -y install build-essential
sudo apt -y install gcc-8 g++-8 gcc-9 g++-9

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8 --slave /usr/bin/g++ g++ /usr/bin/g++-8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9 --slave /usr/bin/g++ g++ /usr/bin/g++-9

sudo update-alternatives --config gcc  
```
  
## 2. NVIDIA 드라이버를 설치
다음 명령으로 현재 사용중인 그래픽 카드에 설치할 수 있는 드라이버를 확인(driver 항목 중 recommended가 붙은 드라이버를 선택)  
```
ubuntu-drivers devices
```
  
해당 버전의 드라이버를 설치한다.  
```
sudo apt install nvidia-driver-450  
```
--> 소프트웨어 & 업데이트 에서 해당 드라이버를 사용하고 있지 않으면 선택 후 재부팅해야한다.  
터미널에서 nvidia-smi 명령을 실행하여 설치한 드라이버 버전이 맞는지 확인  
  
## 3. CUDA Toolkit을 설치
```
sudo apt update  
sudo apt install nvidia-cuda-toolkit  

sudo wget -O /etc/apt/preferences.d/cuda-repository-pin-600 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin  

sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub  
sudo add-apt-repository "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"  

sudo apt install cuda  
```
  
cudnn이 있는지 확인  
```
cat /usr/local/cuda-11.0/include/cudnn.h | grep CUDNN_MAJOR -A 2  
```
  
cudnn이 확인되지 않을 시 https://developer.nvidia.com/rdp/cudnn-archive 에서 다운 받음
```
sudo cp include /cudnn.h /usr/local/cuda-11.0/include  
sudo cp lib64/libcudnn* /usr/local/cuda-11.0/lib64  

sudo chmod a+r /usr/local/cuda-11.0/include/cudnn.h /usr/local/cuda-11.0/lib64/libcudnn*  
```


## PATH에 추가
```
export PATH=/usr/local/cuda-11.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64\
                       ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```  
  
*******************************************************
참고 사이트  
https://webnautes.tistory.com/1428  
https://likecode.tistory.com/306?category=727941  
