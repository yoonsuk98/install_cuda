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
<img width = "550" alt ="Screenshot from 2023-09-03 22-34-42" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/c2a94461-3fcd-4c05-90f2-92bdf961925c">


## 3. CUDA 설치(버전에 맞춰 진행)
<https://developer.nvidia.com/cuda-toolkit-archive> 링크로 이동 후 해당 버전 클릭
<img width = "550" alt ="Screenshot from 2023-09-03 22-47-32" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/836a0bad-a28f-41e4-8bfa-ee37095473ca">

아래와 같이 터미널창에 명령어 입력

<img width = "550" alt ="Screenshot from 2023-09-03 22-48-31" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/55d02499-2d90-4c72-819d-52c6e9e7e293">

```
wget https://developer.download.nvidia.com/compute/cuda/12.2.2/local_installers/cuda_12.2.2_535.104.05_linux.run
```

```
# 파일 권한 설정
sudo chmod 777 cuda_12.2.2_535.104.05_linux.run

# 관리자 권한으로 실행
sudo ./cuda_12.2.2_535.104.05_linux.run
```
조금 기다리면 화면이 나오는데 continue 클릭 → accept입력 → cuda toolkit 제외 전부 x해제 → install 입력 후 기다리면 설치 완료
```
sudo nano ~/.bashrc

# 본인 버전에 맞춰 변경
export PATH=/usr/local/cuda-12.2/bin${PATH:+:${PATH}} 
export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
```
# 재부팅 후 버전이 잘 설치되었는지 확인
nvcc -V
```
<img width = "550" alt ="Screenshot from 2023-09-03 22-35-05" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/32958e55-7074-4b30-a961-933225e91e15">


## 4. cuDNN 설치
<https://developer.nvidia.com/cudnn> 링크로 이후 cuDNN Download 클릭 -> 회원가입 후 로그인

<img width = "550" alt ="Screenshot from 2023-09-03 23-01-47" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/cdb2041c-729f-466d-ae92-273e249fa56f">

그럼 위와 같은 그림이 나오는데 우리는 ubuntu(deb)버전을 다운로드한다.

```
# 다운받은 디렉토리에서 진행

# 다운받은 레포지토리 활성화
sudo dpkg -i cudnn-local-repo-ubuntu2004-8.9.4.25_1.0-1_amd64.deb 

# cuda gpg 키 가져오기
sudo cp /var/cudnn-local-repo-ubuntu2004-8.9.4.25/cudnn-local-4A5BA598-keyring.gpg /usr/share/keyrings/

sudo apt-get update

# 런타임 라이브러리 설치
sudo apt-get install libcudnn8=8.9.4.25-1+cuda12.2

# 개발자 라이브러리 설치
sudo apt-get install libcudnn8-dev=8.9.4.25-1+cuda12.2

# 코드 샘플 설치
sudo apt-get install libcudnn8-samples=8.9.4.25-1+cuda12.2
```

```
# 잘 설치되었는지 확인

sudo find /usr/ -name "cudnn_version.h" # cudnn_version.h 파일 찾아서
cat /usr/include/cudnn_version.h | grep CUDNN_MAJOR -A 2 # 찾은 파일경로로 바꾼 후 확인
```
<img width = "550" alt ="Screenshot from 2023-09-03 22-34-50" src="https://github.com/yoonsuk98/install_cuda/assets/125951880/a101db8e-f402-42bd-ae86-1737ad957a54">

