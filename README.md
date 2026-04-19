## 1. Environment
- [ ] OS : Ubuntu 24.04.4 LTS
- [ ] Shell : Bash
- [ ] Docker Version : 29.3.1
- [ ] Git Version : 2.43.0
## 2.
|Check List|OX|
|:-|:-:|
|Terminal|O|
|Permisson|X|
|Docker|O|
|Dockerfile|X|
|Port|X|
|Volume|X|
|Git|X|
|Github|X|
## 14. 평가기준
절대경로는 사용자가 현재 접근한 디렉토리와는 전혀 관계없이 정혹한 경로를 입력하며 접근하는 기본적인 방법이며 사용자가 처음위치한 루트에서 다른 경로로 이동하고 싶은경우에 
주로 활용하게 됩니다, 
상대경로는 사용자가 현재 접근한 디렉토리를 기준으로 상위 디렉토리 혹은 하위 디렉토리에 위치한 파일에 간편하여 접근하고 싶을때 활용됩니다. 
절대경로와는 달리 사용자가 상세한 경로명을 일일이 적지 않아도 되기 때문입니다.
## 15. 평가기준
파일 권한 표기는 숫자 4,2,1의 조합인 3비트로 표기하며 소유자, 그룹, 기타 순으로 표기합니다.
숫자 4는 읽기, 숫자 2는 쓰기, 숫자 1은 실행권한을 의미합니다.
예를 들어 777=rwxrwxrwx는 소유자, 그룹, 기타에 일기,쓰기,실행 권한이 할당된 것으로 이해할 수 있습니다.
## 오류 해결 내용
### 4월 1일 
도커데스크탑을 deb패키지로 설치하려 했으나 
```
Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root? 
```
같은 메시지가 나오며 설치되지 않아 해결방법을 찾던중 우분투를 재시작 해보라는 글이 있어 따라 해보았습니다. 
그랬더니 도커 데스크톱 버전 확인도 되고, 앱목록에 아이콘도 추가되어, 정상설치가 된줄 알았지만, 터미널과 도커컨테이너에서 hello-world 이미지가 작동되지 않았습니다.
그래서 결국 도커 공식 리포지토리를 우분투에 추가하여 설치하는 방법으로 해결하였습니다.
##
위의 문제를 해결한 다음 제가 이용하는 우분투 버전과 동일한 이미지를 컨테이너에서 실행하려고 docker run ubuntu 24.04.4 를 터미널에 입력했더니
```
docker: Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: exec: "24.04.4": executable file not found in $PATH

Run 'docker run --help' for more information
```
가 나오며 도커 라이브러리에서 풀링과 실행이 되지 않았습니다. 원인을 찾아보니 우분투 버전표기의 가장 마지막에 위치한 .4는 생략해야되는 특징이 있는 것을 알게 되었습니다.
##
### 4월 10일
이미 도커를 설치하고 헬로월드 이미지와 더불어 우분투 이미지가 실행될 컨테이너를 생성하여 실행에 성공했지만 
오늘 다시 container -ls로 생성된 컨테이너들 목록을 확인하려했더니
```
failed to connect to the docker API at unix:///home/almost/.docker/desktop/docker.sock; check if the path is correct and if the daemon is running: dial unix /home/almost/.docker/desktop/docker.sock: connect: no such file or directory
```
위와 같은 오류가 발생되어 도커 데스크탑을 재시작 하는 명령인 systemctl --user restart docker-desktop을 입력하여 이문제를 해결하였습니다.
