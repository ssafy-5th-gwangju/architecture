# architecture   
## 요구 사항 명세서           

* 로그인페이지 -> 회원가입 페이지
* 회원가입 -> 취소 -> 로그인 페이지
* 회원가입 -> 생성 -> 로그인이되고(session storage jwt token) -> 메인으로 
* 메인에서 -> 로그아웃 -> 확인 -> 로그인 (token 삭제)   
* 메인에서 -> 로그아웃 -> 취소    
* 로그인 안 되었는데 메인 -> 로그인        

백엔드 - 테스트 코드 작성  
       
#### 선택 
* 패턴매칭 -> 최소 몇자 이상, 특수문자 제거   
* 비밀번호 찾기 -> 메시지 서비스
* TODOLIST -> CRUD API 
  * 작성한 사람만 수정
  * 작성 안한 사람은 수정 불가능
  * 각 페이지 

# API
## 주소
http://localhost:8080   

## 메인
`/main` GET 방식  

## 공통 요청
### 로그인 정보

* 아이디: devbadak
* 비밀번호: 1234

> 로그인을 하거나 서버가 재시작 되면 인증 토큰이 바뀝니다.

### ContentType

`application/json`

### 인증 방식

헤더 인증방식을 사용한다.

`Authorization: JWT 토큰(Bearer)`   

## 공통 응답     
### 에러 응답

서버에서 `code`, `message`값을 응답한다.

```json
{
    "code": 400,
    "message": "에러 메시지"
}
```

### 폼 검증을 포함한 에러응답

```json
{
    "code": 400,
    "message": "잘못된 요청입니다.",
    
    // 선택  
    "validate": {
        "account": ["1~4글자만 입력할 수 있습니다.", "..."],
        "password": ["비밀번호를 입력해주세요"]
    }
}
```
## 회원 가입
 `/signin`
 
```json
    {
        "id": 1,
        "account": "devbadak",
        "password": "~~~~~~~", 
        "name": "개발바닥",
        "email": "~~@~~~.com"
    }
```  
   
* 아이디 account 
* 패스워드 password
* 이름 name
* 이메일 email -> unique  


## 인증

### 로그인
URI: `/auth/login`  
Method: `POST`

- Request
 
    ```json
    {
        "account": "아이디",
        "password": "비밀번호"
    }
    ```

- Response

    ```json
    {
        "accessToken": "xxx"
    }
    ```

### 로그아웃
URI: `/auth/logout`  
Method: `GET`  

- Response: `status 204`
