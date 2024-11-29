# jtson_dli_snowman
``` bash ```
1. sd카드를 포메터를 다운로드해서 포멧한다

2. 젯펙 링크: ![image](https://github.com/user-attachments/assets/9019dbb5-6ae9-4f73-82db-90f076dd2d42)   해당 링크에서  Jetson Nano Developer Kit SD Card Image를 클릭하여 다운로드한다.

3. balena-echer를 다운로드하여 굽는다.
- 이미지 업로드 후 sd카드에 업로드

4. 연결
- 해당 sd카드를 잿슨나노에 결합한다.
- 키보드와 마우스도 잿슨나노에 연결
- 파워까지 연결하여 작동시작

5. 기본설정
-  기본언어 : 영어
-  와이파이 : aifrenz / 비밀번호 : aifrenz1
-  지도 : 서울
-  name과 password 설정 (우리 조 name: smowman / password : #3515# )
-  continue - continue - continue (즉, 기본값 그대로 3번 연속 continue 클릭)
- next - next - done 누르기

6. 한글 설치
- sudo apt-get update 입력 후 엔터
- sudo apt-get install fcitx-hangul 입력 후 엔터
- m-config -n fcitx 입력 후 엔터 
- reboot 입력 후 엔터
- all setting - language support
  ![image](https://github.com/user-attachments/assets/46b4ed6d-27be-4bd3-bf3a-55f5d64a7da3)
- install
  ![image](https://github.com/user-attachments/assets/ae4b5c9b-4d69-44af-b62a-c3384c41a072)
- keyboard input method system 항목을 fcitx로 변경
  ![image](https://github.com/user-attachments/assets/545d3ede-1aa3-4c6e-9db7-83fe83d1684b)
- 우상단 키보드모양에서 figure - "+" 버튼 
  ![image](https://github.com/user-attachments/assets/ace5c8a2-8343-4eb3-bbc6-f56f9adbfb1e)
- Only Show Current Language 체크해제 - hangul 검색
  ![image](https://github.com/user-attachments/assets/928df151-be25-4a6e-9ca6-6372827345d1)
- Input Method Configuration의 Global Config 탭(tab)을 클릭한다.
- Trigger Input Method의 왼쪽 버튼을 마우스 클릭한다음 "한영키"를 누르기.
  ![image](https://github.com/user-attachments/assets/b44aeabb-f0ac-4de5-b978-5a98c83a54df)




- **잘 됐는지 확인 작업:  입력이 한글로 될 때 우상단에 태극문양이 나오는 것을 확인할 수 있을것.**




2번째 수업

1. 버전확인
- Terminal을 열어준다.
- sudo apt install python3-pip 입력
- do you want to continue ? Y
- sudo -H pip3 install -U jetson-stats
jetson-stats-4.2.3 가 써진 걸 확인.
**만약 에러가 나온다면 ??? ** sudo apt-get upgrade / sudo apt-get update  진행


2. 온도체크 및 쿨링
- jtop 으로 온도체크 / **만약 온도가 높다면??? ** 쿨링팬 장착
- sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'   <<<< 해당코드로 인해 10도 정도 떨어지기도 함

3. 카메라
- Terminal 열어주기
- ls /dev/vi*  <<<<<젯슨이 카메라를 인식하는지 알 수 있는 코드
- git clone https://github.com/jetsonhacks/USB-Camera.git
- 만약 usb로 카메라를 외부에서 연결했다면 dli@dli-desktop:~$ cd USB-Camera
- 만약 내부 장착 카메라일 경우 dli@dli-desktop:~$ cd CSI-Camera
- ex)
입력코드
dli@dli-desktop:~/USB-Camra$ ls
결과
face-detect-usb.py  LICENSE  README.md  usb-camera-gst.py  usb-camera-simple.py    

윗 줄 중 하나를 끌고 온다.
dli@dli-desktop:~/USB-Camera$ python3 usb-camera-gst.py

결과 사진


8. Docker 및 swap 설치
- dli@dli-desktop:~$ ls   >>> 확인
- dli@dli-desktop:~$ mkdir -p ~/nvdli-data >>>>교육과정에 필요한 dir 추가하기
- dli@dli-desktop:~$ ls    >>> 추가되었는지 확인하기
- dli@dli-desktop:~$#!/bin/bash
- sudo docker run --runtime nvidia -it --rm --network host \
    --memory=500M --memory-swap=4G \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --volume /tmp/argus_socket:/tmp/argus_socket \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr

  >>>>>> 우리 조의 경우 이미 SD카드 속에 docker와 swap이 된 상태였으므로 바로 결과가 나옴.


--------------------------------------------------------------

9. classification
- 컴퓨터 웹브라우저를 열고 주소창에 192.168.55.1:8888  을 입력.
- 주피터에 있는 코드 실행
- (세부과정)
- 카메라 종류에 맞게 import 시키기
- 데이터 수집도구 위젯 만들기
- 뉴럴네트워크 정의, 레이어 조정
- 실시간 실행위젯 설정
- 트레이너 정의 및 제어
- 대화형 위젯 만들고 표시
- 
- **아래 과정이 중요**
- 카테고리를 thumbs_up으로 설정 -> 카메라로 엄지를 위로 올린 상태를 찍으면서 add -> count를 30이 될 때까지 진행 (여기서 다양한 각도와 위치에서 촬영하는 것이 중요)
-> 카테고리를 Thumbs_down으로 설정 후 엄지를 아래로 둔 상태로 add -> count를 30이 될 때까지 진행 -> epochs 10 으로 설정 후 train
- 결과확인 : 
  카메라에 엄지를 위로 올렸을 때 Thumbs_up 이 1.0 이 되며 Thumbs_down이 0이 되면 best
  반대로도 되는지 확인


