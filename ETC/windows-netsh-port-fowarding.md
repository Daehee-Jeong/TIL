## 윈도우 환경에서 netsh 명령어를 사용하여 포트포워딩 하기

사내 위키를 윈도우 서버 내 구축하며 포트포워딩 설정이 필요하여 확인한 내용.

ex) **80**포트로 들어온 모든 요청을 **81**포트로 포워딩 하는 경우.

설정방법은 다음과 같다. 

```
netsh interface portproxy add v4tov4 listenport=80 connectport=81 connectaddress=(내부로 연결할 IP주소)
```
확인방법은 다음과 같다.

```
netsh interface portproxy show v4tov4
```