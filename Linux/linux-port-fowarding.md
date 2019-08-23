## 리눅스 포트포워딩 설정하기

예시로 80포트로 들어오는 모든 요청을 8080포트로 포워딩하는 방법입니다.

```sh
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```