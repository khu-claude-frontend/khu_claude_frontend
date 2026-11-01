# 09 라우터 골격과 `dependencies.dart` 조립

## 목표

B·C가 서로의 코드를 참조하지 않고도 화면을 연결할 수 있도록 경로와 이름을 먼저 정한다.

## 할 일

- [ ] URL 방식 결정(path / hash). path면 배포 서버가 모든 경로를 `index.html`로 돌려줘야 한다
- [ ] `lib/app/router.dart`: 사용자·관리자(`/admin/…`) 경로 분리
- [ ] 화면별 라우트 이름 상수 정의. 각 경로에는 담당자가 채울 임시 페이지를 둔다
  - 사용자: 시작(US-00), 검색 조건 단계(US-01·02), 출발 건물 선택(US-03), 후보 상세(US-04), 결과 없음(US-05), 길찾기·내부 안내(US-06 A·B), 이용 중(US-06 C), 이용 의견(US-07 A·B), 재조사 요청(US-07 C)
  - 관리자: 로그인(AD-01), 공간 목록(AD-02), 등록·수정(AD-03), 공간 상세·재조사 처리(AD-04)
- [ ] 화면 간 넘겨줄 값(예: 공간 ID) 정의. B → C로 넘어가는 지점은 '공간에 도착했어요' → 이용 중 화면이다
- [ ] 관리자 로그인 가드가 들어갈 `redirect` 자리 마련(가드 구현은 C)
- [ ] `lib/app/dependencies.dart`: API Client 생성과 `provider` 연결. Repository 구현체는 B·C가 여기에 추가한다

## 완료 조건

- 모든 경로가 임시 페이지로 열린다
- 라우터 경로에 대한 Widget Test가 있다

## 참고

- `docs/architecture.md` 디렉터리별 역할(`lib/app/`), 의존성 규칙
- `docs/tasks/README.md` B·C 작업 목록
