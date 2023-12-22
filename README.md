# HOW TO INSTALL_CUDA
How to availiable cuda in linux / windows

cuDNN을 사용하기 위해 Cuda가 필요하고 Cuda를 사용하기 위해서 nvidia 드라이버가 필요하다. 
이에 세가지 버전 모두 호환이 가능해야한다. 

그러나 호환되는 버전을 찾을 때 어려움이 많다.

이에 여러 어려움을 없애고자 일단 본인 그래픽카드와 관련된 nvidia-driver를 찾아서 설치하면,
관련 cuda 버전이 나오는데 이를 확인 후 해당 버전을 설치하면 된다.

## 1. Graphic 카드 버전 확인
```
lspci | grep -i VGA
```
   
## 2. Nvidia-Driver 설치
```
# 본인이 설치해야할 드라이버 버전 숫자 변경
# 설치 중 블랙스크린 나올 가능성 존재. 그러나 당황하지 말고 블랙스크린상태에서 약 3분정도 기다린 후 강제종료 후 재부팅 진행 

sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-driver-535
```

```
# 설치확인

nvidia-smi
```

## 3. CUDA 설치

