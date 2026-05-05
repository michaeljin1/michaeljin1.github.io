# 프로젝트 페이지 디자인 가이드

각 프로젝트 팝업 페이지(`projects/*.html`)는 **하나의 가이드**를 따릅니다.
새 프로젝트 추가 / 기존 프로젝트 정리 시 이 문서를 기준으로 합니다.

> Reference: `projects/yt.html` (유튜브 분리수거)

---

## 1. 헤더 / 페이지 구조

- ❌ **상단 `proj-back` 헤더 사용 금지** (← 양영진 / 메타 표시)
  - 이유: index.html에서 모달로 띄우는 팝업이라 중복 정보
- ✅ `<body>` 바로 아래 `<article class="section project tile-XXX">` 로 시작
- ✅ 단일 페이지 스크롤 — **외부 페이지로 빠지는 링크 금지**
  - 모든 콘텐츠 (아키텍처, 화면, 상세 설명) 한 페이지 안에 inline

---

## 2. 폰트

```html
<link rel="preconnect" href="https://cdn.jsdelivr.net" crossorigin>
<link rel="stylesheet" as="style" crossorigin
      href="https://cdn.jsdelivr.net/gh/wanteddev/wanted-sans@v1.0.3/packages/wanted-sans/fonts/webfonts/variable/split/WantedSansVariable.min.css" />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>
  body, body * {
    font-family: "Wanted Sans Variable", "Wanted Sans",
                 "DM Sans", -apple-system, BlinkMacSystemFont,
                 system-ui, "Apple SD Gothic Neo", "Noto Sans KR", sans-serif !important;
    letter-spacing: -0.005em;
  }
</style>
```

- **한국어**: Wanted Sans Variable
- **영문/숫자**: DM Sans
- 시스템 fallback: Apple SD Gothic Neo / Noto Sans KR
- `letter-spacing -0.005em` 미세 조정

---

## 3. 페이지 흐름 (위에서 아래로)

```
1. <header class="project__head">          — 제목 + 태그라인 (chips는 사용 X, 인트로 stack으로 대체)
2. 인트로 (.yt-intro)                       — 좌: lede 한 문단 / 우: Stack 카드 (그룹별)
3. 실제 화면 (.yt-shots)                    — mockup 4개 (2x2 그리드)
4. 시스템 아키텍처 (.mini-arch)             — 4-layer 미니 다이어그램
5. (선택) 처리 흐름 (.yt-flow)              — 단계별 시간 표시
6. 외부 링크 1줄                            — 라이브 사이트 / GitHub 등
```

---

## 4. 인트로 섹션 — 앱 설명 + 스택

### 좌측: lede
- 1~2문단, 제품의 한 줄 정의 + 핵심 기능
- 굵은 표시는 **strong** 태그로 핵심 키워드만

### 우측: Stack 카드 (`.yt-stack`)
그룹별로 정리:
- Frontend
- Backend
- AI · Data
- Infra · 결제

각 그룹 안에 작은 칩으로 라이브러리/서비스 나열.

---

## 5. 실제 화면 — Mockup 가이드

- **2x2 그리드** (`.yt-shots`)
- 각 mockup은 **CSS로 구현** (실제 스크린샷 없을 시)
- ❌ **캡션 설명 (.yt-shot__desc) 사용 금지**
  - Label (Step 1) + Title (URL 입력)만 표기
  - 길게 설명하지 않음 — 시각적으로 전달
- 화면 종류 예시:
  1. 입력 화면
  2. 진행/로딩 화면 (스트리밍, 분석 중)
  3. 결과 카드/리스트
  4. 상세 모달

---

## 6. 시스템 아키텍처 — 미니 다이어그램

`.mini-arch` 클래스로 inline 구성:
```
사용자 (1열)
   ↓
Frontend / Auth / CDN (3열)
   ↓
Backend Pipeline / Auth / Webhook (3열)
   ↓
External APIs / DB (4열)
```

- 노드 색상으로 레이어 구분 (`--primary` / `--orange` / `--purple`)
- ❌ **"전체 다이어그램 보기 →" 같은 외부 링크 금지** — 이 미니가 곧 전부

---

## 7. 처리 흐름 (선택)

`.yt-flow`로 번호 매겨진 단계 리스트:
- 각 단계: 번호(파란 원) + 제목 + 시간 표시 + 한 줄 설명
- 시간은 `tnum` (tabular numbers) 적용
- 영상/요청 1개 처리 시 시간 분포 보여줌

---

## 8. 콘텐츠 금지 항목

다음 섹션은 **프로젝트 팝업에 넣지 않음** (이력서/자기소개에 따로 정리):

- ❌ "배운 점 — XXX" 시리즈
- ❌ "시행착오와 의사결정"
- ❌ 자기소개 / 강점 어필 문구
- ❌ "결과 / 지표" 표 (수치 자랑)
- ❌ "향후 로드맵"

→ **객관적 사실만**: 무엇을 만들었나 + 어떻게 작동하나 + 어떤 화면인가

---

## 9. 디자인 토큰

기존 `styles.css` 변수 그대로 사용:
- `--primary: #0066cc`
- `--ink: #1d1d1f`
- `--canvas: #ffffff`
- `--parchment: #f5f5f7`
- `--hairline: #e5e5e7`
- `--muted: #6e6e73`
- 등급 색: green `#34c759` / orange `#ff9500` / red `#ff3b30`

---

## 10. 적용 체크리스트

새 프로젝트 추가 시:
- [ ] proj-back 헤더 없음
- [ ] 폰트 link + style 추가됨
- [ ] 인트로 좌(lede) + 우(stack) 구조
- [ ] 실제 화면 mockup 2~4개 (캡션 1줄)
- [ ] 미니 아키텍처 (해당되면)
- [ ] 처리 흐름 (해당되면)
- [ ] 외부 페이지 링크 0개
- [ ] 배운 점/이력서 콘텐츠 0개
- [ ] 외부 라이브 링크 1줄 (있으면)

---

## Reference

`projects/yt.html` 을 참고 템플릿으로 사용. 새 프로젝트는 yt.html 복사 후 콘텐츠만 교체하는 것이 가장 빠름.
