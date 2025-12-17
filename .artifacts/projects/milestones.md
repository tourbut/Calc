# Project Milestones

이 문서는 프로젝트의 주요 마일스톤과 각 단계별 핵심 작업 내용을 정의합니다.

## Phase 1: Foundation (기반 구축)
**목표**: 개발 환경을 세팅하고, 백엔드/프론트엔드/DB가 연동되는 "Hello World" 수준의 통합 환경을 구축합니다.

### 1.1 Repository & Environment Setup
- [ ] Git Repository 초기화 및 `.gitignore` 설정
- [ ] `uv` 기반 Python 백엔드 프로젝트 구조 생성 (`backend/`)
- [ ] `npm` 기반 SvelteKit 프론트엔드 프로젝트 구조 생성 (`frontend/`)
- [ ] Docker Compose 설정 (PostgreSQL, Redis 포함)

### 1.2 Database & Architecture Skeleton
- [ ] PostgreSQL 컨테이너 구동 확인
- [ ] SQLAlchemy/SQLModel 기반 DB 연결 설정 (`core/config.py`, `db/session.py`)
- [ ] Alembic 초기 설정 및 첫 번째 마이그레이션 테스트

### 1.3 Basic API & UI Connection
- [ ] FastAPI Health Check API 구현 (`/api/health`)
- [ ] SvelteKit에서 백엔드 API 호출 테스트 페이지 작성
- [ ] Docker Compose로 전체 서비스(Back, Front, DB) 동시 실행 확인

---

## Phase 2: Core Domain & Auth (핵심 도메인 및 인증)
**목표**: 사용자 인증 시스템을 구축하고, 프로젝트의 핵심 도메인 모델을 설계 및 구현합니다.

### 2.1 Authentication (Auth)
- [ ] User 모델 정의 (Email, Password, Role 등)
- [ ] JWT 기반 로그인/회원가입 API 구현
- [ ] 프론트엔드 로그인 페이지 및 인증 상태 관리 (Store) 구현

### 2.2 Core Domain Implementation
- [ ] `domain_rules.md`에 정의될 핵심 도메인 엔티티 모델링
- [ ] 핵심 도메인에 대한 CRUD API 구현
- [ ] 프론트엔드 핵심 기능 UI 구현 및 연동

---

## Phase 3: Advanced Features & Optimization (고도화)
**목표**: 캐싱, 비동기 작업 등 성능과 안정성을 위한 기능을 추가하고, 비즈니스 로직을 완성합니다.

### 3.1 Caching & Performance
- [ ] Redis 설정 및 캐싱 전략 적용 (자주 조회되는 데이터)
- [ ] API 응답 속도 최적화

### 3.2 Background Tasks (Optional)
- [ ] Celery + Redis Message Broker 설정
- [ ] 비동기 작업(이메일 발송, 데이터 집계 등) 구현

---

## Phase 4: Stability & Deployment (안정화 및 배포)
**목표**: 테스트 코드를 작성하고, 프로덕션 배포를 위한 준비를 마칩니다.

### 4.1 Testing
- [ ] Pytest 기반 백엔드 유닛/통합 테스트 작성
- [ ] 프론트엔드 주요 컴포넌트 테스트

### 4.2 CI/CD & Deployment
- [ ] GitHub Actions 등 CI 파이프라인 구성 (Lint, Test)
- [ ] Docker Image 빌드 및 배포 스크립트 작성 (`start.sh`, `Dockerfile` 최적화)
- [ ] Nginx 리버스 프록시 및 SSL 설정
