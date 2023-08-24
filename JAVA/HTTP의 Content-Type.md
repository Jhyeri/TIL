
# 📌 Content-Type이란?

- HTTP 헤더에 명시되는 타입을 말한다.
- 클라이언트 → 서버로 POST 요청 시 body에 데이터를 담거나, 
서버 → 클라이언트로 데이터를 담아서 응답할 때,
**해당 데이터의 타입을 나타내기 위해** 사용한다.

    #### 💡 HTTP 헤더란?
    <aside>
    클라이언트, 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 해준다.
    
    </aside>
<br/>

# 📌 클라이언트에서 사용하는 Content-Type

API 요청 시, 서버로 데이터를 전송할 때 클라이언트에서 사용하는 Content-Type은 주로 3가지이다.

### 1. application/x-www-form-urlencoded

- `key=value` 의 형태로 표현한다.
- ‘&’ 기호로 분리한다.

#### 쿼리스트링 vs application/x-www-form-urlencoded

- 데이터 포맷은 같다.
- 쿼리스트링은 body가 아닌, URL 뒤에 붙여서 전송된다.
- application/x-www-form-urlencoded은 POST 전송 시 body에 데이터가 담겨 전송된다.

### 2. multipart/form-data

- 단일 본문에 하나 이상 여러 종류의 데이터 파트가 포함되며, 파일 업로드에 많이 사용된다.
- 각 데이터들을 개행과 바운더리 문자열로 구분한다.

### 3. application/json

- API 개발 시 가장 많이 사용되는 Content-Type
- body에 json 포맷으로 데이터가 담긴다.
