# 06 API Client와 RFC 9457 에러 파싱

## 목표

B·C의 Repository 구현체가 쓰는 HTTP 클라이언트와 공통 예외를 `lib/core/network/`, `lib/core/errors/`에 만든다.

## 할 일

- [ ] Base URL: 웹과 API가 같은 도메인이므로 현재 origin 기준으로 `/api/v1/…`를 호출한다
- [ ] 로컬 개발에서 같은 도메인을 맞추는 방법 결정(개발 서버 프록시 등). 세션 쿠키(`sid`, `asid`)가 HttpOnly라 다른 origin으로는 붙지 않는다
- [ ] JSON 요청·응답 처리(`Content-Type: application/json`)
- [ ] `application/problem+json` 파싱 → 공통 예외(`AppException`)
  - `type` URI 끝의 slug로 구분한다. 화면에 `detail`을 그대로 띄우지 않는다
  - 확장 멤버 `errors[]`(`pointer` / `parameter`), `account`(`not-in-admin-list`)
  - `type`이 없으면(`about:blank`) 상태 코드로 구분
  - 5xx는 본문과 상관없이 상태 코드로 처리한다. `502`·`504`는 problem+json이 아닐 수 있다
  - `429`·`503`의 `Retry-After` 헤더
- [ ] 관리자 API의 `401`을 C가 받아 AD-01로 보낼 수 있도록 알림 지점 제공

## 완료 조건

- 정상 응답, problem+json, `about:blank`, problem+json이 아닌 5xx에 대한 Unit Test가 있다

## 참고

- API 명세 1.1 공통 규칙, 1.2 에러 응답 형식, 1.3 상태 코드 사용 원칙, 7장 에러 유형
