# Project: Smart Web Calculator (스마트 웹 계산기)

## 1. 목적 (Purpose)
- **사용자 가치**: 기본적인 사칙연산부터 공학용 기능까지 웹 브라우저에서 즉시 사용 가능한 직관적인 계산 도구를 제공합니다.
- **기술적 목표**:
    - **AI 협업 검증**: 사전에 정의된 'Version Control Guidelines'와 'Conventional Commits'를 준수하며 AI 에이전트와 협업하는 워크플로우를 확립합니다.
    - **품질 확보**: TypeScript 기반의 타입 안전성과 Jest를 이용한 단위 테스트(Unit Test) 커버리지를 확보합니다.
    - **배포 자동화**: GitHub Actions를 통해 `main` 브랜치 병합 시 자동 배포되는 CI/CD 파이프라인을 구축합니다.

## 2. 주요 기능 (Key Features)

### 2.1. 표준 연산 (Standard Operations)
- **사칙연산**: 덧셈(+), 뺄셈(-), 곱셈(×), 나눗셈(÷)의 정확한 부동소수점 연산 처리.
- **기본 제어**:
    - `AC` (All Clear): 모든 입력 및 결과 초기화.
    - `C` (Clear): 마지막 입력값 지우기.
    - `+/-`: 양수/음수 부호 전환.
    - `%`: 백분율 변환.

### 2.2. 고급 기능 (Advanced Features)
- **계산 기록 (History)**:
    - 최근 10개의 계산 수식과 결과를 사이드 패널에 리스트 형태로 표시.
    - 기록 클릭 시 해당 수식이나 결과를 현재 입력창으로 불러오기.
- **키보드 지원**: 마우스 클릭 외에 Numpad 및 키보드 입력을 통한 연산 지원 (Enter = 결과 도출, Esc = 초기화).

### 2.3. UI/UX
- **반응형 디자인**: 데스크탑, 태블릿, 모바일 환경에 맞춰 레이아웃 자동 조정.
- **다크/라이트 모드**: 시스템 설정 감지 및 사용자 토글 버튼을 통한 테마 변경 (Tailwind CSS 기반).

## 3. 비기능 요구사항 (Non-functional Requirements)

### 3.1. 기술 스택 (Tech Stack)
- **Frontend**: Svelte, TypeScript, Vite
- **Styling**: Tailwind CSS,Flowbite-Svelte
- **Test**: Jest, Svelte Testing Library

### 3.2. 품질 및 성능 (Quality & Performance)
- **Floating Point Precision**: `decimal.js` 라이브러리를 사용하여 자바스크립트 부동소수점 오류(0.1 + 0.2 != 0.3) 방지.
- **Test Coverage**: 핵심 연산 로직(Logic Layer)에 대해 테스트 커버리지 90% 이상 유지.
- **Linting**: ESLint, Prettier 설정을 통해 AI가 생성한 코드의 스타일 통일.

## 4. 참고 자료 (References)

- **Design Reference**:
    - [Apple Calculator Design](https://support.apple.com/ko-kr/guide/calculator/welcome/mac) (심플함 참조)
    - [Google Calculator UI](https://www.google.com/search?q=calculator) (웹 접근성 참조)
- **Library Documentation**:
    - [Math.js Docs](https://mathjs.org/docs/index.html) (정밀 연산 라이브러리)
    - [React Docs](https://react.dev/)
- **Internal Guidelines**:
    - `Version Control Guidelines.md` (프로젝트 루트에 위치)
    - `CHANGELOG.md` (자동 생성 예정)