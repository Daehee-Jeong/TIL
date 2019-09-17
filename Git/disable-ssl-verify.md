## Git 사용 시 SSL 인증절차 해제 방법

**사설인증서**를 사용하는 Git 서버의 repository를 clone 하거나 push, pull 등의 작업을 할 시 오류가 발생할 수 있습니다.

에러는 다음 스크린샷과 같이 발생하게 됩니다.
![CSRF 구글 검색 결과](/images/disable-ssl-verify-01.png)

해결은 `http.sslVerify` 속성 설정을 통해 가능합니다.

```sh
git config http.sslVerify false
```

저의 경우에는 이미 로컬에 존재하는 repository가 아닌 clone을 받아야하는 경우였습니다.
따라서 `--global` 옵션으로 전역설정을 false로 하였고, clone을 받은 뒤 전역 설정을 원래대로 돌려놓았습니다.
(clone한 repository는 **false**로 설정)

부가적으로, `http.sslVerify` 옵션은 git 내부적으로 `libcurl` 호출시 SSL 검증을 하지 않도록 작동됩니다.

___

___

>**수정이력**  
2019.09.17 최초작성

>**출처 및 참고**  
https://www.lesstif.com/pages/viewpage.action?pageId=14090808