# SPRING ADVANCED
---

## 🛠️ 주요 구현 사항

### 📌 레벨 0: 프로젝트 설정
* **설정 및 오류 해결**
    * `application.properties` 누락 및 JWT 시크릿 키 설정 오류 해결
    * `application.properties` DB 연결 오류 해결
* **참고 자료 / 트러블 슈팅**
    * 관련 트러블 슈팅 기록: 
  [Velog 링크](https://velog.io/@luke1495/TIL-프로젝트-세팅-트러블-슈팅)

---

### 📌 레벨 1: ArgumentResolver
* **핵심 구현 내용**
    * Spring Bean 등록을 위한 `@Component` 어노테이션 추가
    * `WebMvcConfig` 설정 추가 및 Custom `ArgumentResolver` 등록

* **참고 자료 / 트러블 슈팅**
  * 관련 트러블 슈팅 기록:
  [Velog 링크](https://velog.io/@luke1495/TIL-ArgumentResolver-트러블-슈팅)

---
### 📌 레벨 2: 코드 개선
* **핵심 구현 내용**
  * 이메일 검증이 가장 먼저 실행되고 그후 사용자 역할과 비밀번호의 암화화 로직이 오도록 순서를 변경
  * 불필요한 if-else 대신 2개의 if문으로 변경
  * 유효성 검증을 DTO에서 실행하기 위해 UserService내 로직 수정,
  <br> UserChangePasswordRequest내 검증을 위한 어노테이션과 검증 조건 추가, UserController에서 관련 부분 @RequestBody 뒤에 @Valid
를 추가

---

### 📌 레벨 3: N+1 문제
* **핵심 구현 내용**
  * TodoRepository에서 `fetch join` 을 사용하여 N+1을 해결하고 있던 코드를 `@EntityGraph`를 사용하여 
  <br> 동일한 동작을 하도록 수정

---

### 📌 레벨 4: 테스트 코드 연습
* **핵심 구현 내용**
  * `PasswordEncoderTest` 클래스에 있는 passwordEncoder.matches의 인자 순서를 rawPassword, encodedPassword 순으로 변경하여
  <br> 인자 순서 불일치를 해결
  * `ManagerServiceTest` 클래스에 있는
   `manager_목록_조회_시_Todo가_없다면_InvalidRequestException_에러를_던진다()`로 변경하고
  <br> "Manager not found"를 "Todo not found"로 변경하여 예외 메세지 불일치 해결
  * `CommentServiceTest` 쿨래스에 있는
    `ServerException exception` 을 `InvalidRequestException`로 변경하여
  <br> MangerService 예외 처리 불일치를 해결
  * `MangarServic` 클래스에 있는
  saveManager 메서드에서 todo.getUser() == null를 추가
  <br> if (todo.getUser() == null || !ObjectUtils.nullSafeEquals(user.getId(), todo.getUser().getId())) 로 수정하여
  <br>Todo의 User가 null일 경우 예외처리가 발생하도록 변경 

* **참고 자료 / 트러블 슈팅**
  * 관련 트러블 슈팅 기록:
    [Velog 링크](https://velog.io/@luke1495/TIL)
  
---

## 📂 기술 Stack
* **Language:** Java
* **Framework:** Spring Boot / Spring MVC
* **Build Tool:** Gradle
* **Environment:** IntelliJ IDEA, Windows (PowerShell, Git)