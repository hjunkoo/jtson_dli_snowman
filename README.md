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
-  continue - continue - continue
  여기에 캡쳐사진 넣기
- next - next - done 누르기
  캡쳐
- 


4. 한글 설치
- sudo apt-get update
- sudo apt-get install fcitx-hangul
- m-config -n fcitx
- reboot
- laugauage (동영상확인)
-  keyboard input method system 항목을 fcitx로 변경
-  우상단 키보드모양에서 figure - "+" 버튼 - hangul 검색
- Input Method Configuration의 Global Config 탭(tab)을 클릭한다.
- Trigger Input Method의 왼쪽 버튼을 마우스 클릭한다음 "한영키"를 누르기.




2번째 수업

5. 버전확인
- sudo apt install python3-pip
- do you want to continue ? Y
- sudo -H pip3 install -U jetson-stats
jetson-stats-4.2.3 가 써진 걸 확인.

6. 온도체크 및 쿨링
- jtop 으로 온도체크 / 만약 높다면 쿨링팬 장착
- sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'   <<<< 해당코드로 인해 10도 정도 떨어지기도 함

7. 카메라
- ls /dev/vi*  <<<<<제슨이 카메라를 인식하는지 알 수 있는 코드
- git clone https://github.com/jetsonhacks/USB-Camera.git
- 만약 usb로 카메라를 외부에서 연결했다면 dli@dli-desktop:~$ cd USB-Camera
- 만약 내부 장착 카메라일 경우 dli@dli-desktop:~$ cd CSI-Camera
ex)
dli@dli-desktop:~/USB-Camra$ ls

face-detect-usb.py  LICENSE  README.md  usb-camera-gst.py  usb-camera-simple.py    

윗 줄 중 하나를 끌고 온다.

dli@dli-desktop:~/USB-Camera$ python3 usb-camera-gst.py

결과 사진



