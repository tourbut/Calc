# Tech Stack

## Backend

- **Language:** Python 3.13 (latest)
- **Framework:** FastAPI
- **ORM / DB Layer:**
  - SQLAlchemy (Async)
  - SQLModel (타입 안정성과 선언적 모델 정의를 위해 사용)
- **Server Runtime:**
  - uv (패키지/환경 관리)
  - uvicorn (ASGI 서버)

### Backend Structure
```
backend
├── Dockerfile                  # 백엔드 컨테이너 빌드 설정
├── alembic.ini                 # Alembic DB 마이그레이션 설정
├── app/                        # 메인 애플리케이션 코드
│   ├── main.py                 # FastAPI 앱 엔트리포인트 (앱 실행, 미들웨어)
│   ├── core/                   # 핵심 설정 및 유틸리티
│   │   ├── config.py           # 환경 변수 및 앱 설정
│   │   └── RedisManager.py     # Redis 연결 및 관리
│   ├── models/                 # 데이터베이스 모델 (SQLModel)
│   │   ├── __init__.py         # 모델 초기화
│   │   ├── model1.py           # 모델 1
│   │   ├── model2.py           # 모델 2
│   │   └── model3.py           # 모델 3
│   ├── src/                    # 비즈니스 로직 및 API 구현
│   │   ├── api.py              # API 라우터 통합
│   │   ├── routes/             # API 엔드포인트 핸들러
│   │   ├── crud/               # 데이터베이스 CRUD 함수
│   │   ├── schemas/            # Pydantic 데이터 검증 스키마
│   │   ├── engine/             # 핵심 엔진 로직 (AI, 백그라운드 작업 등)
│   │   ├── deps.py             # 의존성 주입 (DB 세션, 인증 등)
│   │   └── utils/              # 기타 유틸리티 함수
│   └── alembic/                # 마이그레이션 스크립트 저장소
├── config/                     # 서버 실행 관련 스크립트
│   ├── start.sh                # 서버 시작 스크립트
│   └── gunicorn_conf.py        # Gunicorn 설정
└── files/                      # 업로드된 파일 또는 임시 파일 저장소
```

## Environment & Execution Context (중요)
**에이전트가 코드를 실행하거나 디버깅할 때 반드시 참고해야 할 환경 설정입니다.**
- **Package Manager:** `uv`
  - 모든 패키지 설치 및 관리는 `uv add`, `uv remove` 등을 사용합니다.
  - 가상환경(`venv`)은 backend의 `.venv`에 위치합니다.
- **PYTHONPATH Strategy:** 
  - 소스 코드는 프로젝트 루트 아래 `backend/app` 디렉토리에 위치합니다.
  - **실행 명령:** 스크립트 실행 시 반드시 **프로젝트 루트**에서 `uv run` 명령어를 사용합니다. `uv`는 자동으로 `app`를 `PYTHONPATH`에 포함시킵니다.
    - 예: `uv run uvicorn app.main:app --reload` (O)
    - 예: `cd app && python main.py` (X - 경로 오류 발생 원인)
- **Import Style:**
  - 모든 import는 `app`를 기준으로 한 **절대 경로**를 사용합니다.
  - 예: `from app.core.config import settings`

## Frontend

- **Framework:** Svelte, SvelteKit
- **Language:** TypeScript
- **UI / 스타일링:**
  - Tailwind CSS
  - Flowbite (Tailwind 기반 UI 컴포넌트 라이브러리)
- **Serving:**
  - nginx를 사용하여 정적 파일/리버스 프록시 구성

## Database

- **PostgreSQL**
  - 메인 트랜잭션 데이터 저장소로 사용
  - 자산, 포지션, 사용자 계정 등 핵심 도메인 데이터 저장

## Cache

- **Redis**
  - 자주 조회되는 정보 캐싱
  - 세션/레이트 리밋 관리 등에 활용 가능

## Asynchronous / Background Tasks

- **Celery**
  - 무거운 작업이 필요한 경우 백그라운드 태스크로 처리
  - Redis를 사용하여 작업 큐 관리

## Infrastructure

- **Docker Compose**
  - Backend, Frontend, PostgreSQL, Redis, (필요 시) Celery Worker/Beat, nginx를 컨테이너로 구성
  - 개발 환경에서 `docker compose up` 한 번으로 전체 스택을 기동할 수 있도록 설계