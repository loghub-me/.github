# LogHub

![bento](https://raw.githubusercontent.com/loghub-me/.github/master/images/bento.webp)

> [**loghub.me**](https://loghub.me)

#### Repositories

[![GitHub Repo](https://img.shields.io/badge/GitHub-Web-f94949?style=plastic&logo=github)](https://github.com/loghub-me/web-next)
[![GitHub Repo](https://img.shields.io/badge/GitHub-API-6db240?style=plastic&logo=github)](https://github.com/loghub-me/api)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Task_API-aab2ff?style=plastic&logo=github)](https://github.com/loghub-me/task-api)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Markdown_Renderer-2d79c7?style=plastic&logo=github)](https://github.com/loghub-me/markdown-renderer)

## 소개

LogHub는 개발자들이 지식을 공유하고, 서로의 경험을 나누는 플랫폼입니다.

**주요 기능**은 다음과 같습니다:

- `아티클` : 블로그 형태로 기술적인 내용을 공유하는 공간입니다. 댓글 기능을 포함합니다.
- `시리즈` : 여러 개의 챕터를 포함하는 아티클의 모음입니다. 리뷰 기능을 포함합니다.
- `질문과 답변` : 개발자들이 질문을 올리고 답변을 받을 수 있는 공간입니다. LLM 기반의 답변 생성 봇 기능을 포함합니다.

**부가 기능**은 다음과 같습니다:

- `검색` : 검색 엔진을 사용하여 아티클, 시리즈, 질문 그리고 토픽을 검색할 수 있습니다.
- `토픽` : 아티클, 시리즈, 질문에 토픽을 추가하여 관련된 포스트를 그룹화할 수 있습니다.
- `스타` : 즐겨찾기 기능으로 관심있는 아티클, 시리즈, 질문을 저장할 수 있습니다. (GitHub-like)
- `활동` : 사용자의 활동을 잔디뷰 형태로 확인할 수 있습니다. (GitHub-like)
- `Markdown 지원` : 아티클, 시리즈, 질문 작성 시 마크다운을 지원합니다. (에디터 및 렌더링)

## 사용 언어 및 프레임워크

- `프론트엔드` : Next.js, TypeScript, pnpm, TailwindCSS, shadcn/ui
- `백엔드` : Spring Boot, Kotlin, Gradle, ElysiaJS, Bun
- `데이터베이스` : PostgreSQL(+PGroonga), Redis
- `기타` : Cloudflare R2, Resend, GitHub Actions, Docker, GCP

## 주요 개발 내용

> [!NOTE]
> 핵심 성과: 검색 성능 **13% 향상**, 상세 조회 성능 **82% 향상**,  
> **Password-less** 인증 시스템 구현, **LLM** 기반 질문 답변 봇 구현

### 검색

- PGroonga 기반 검색 시스템으로 Elasticsearch 대체 → 검색 성능 13% 향상 및 데이터 일관성 확보
- Redis를 사용하여 마크다운 렌더링 결과 캐싱 → 캐싱 후, 조회 + 마크다운 렌더링 API 성능 82% 향상
- Redis ZSet을 사용하여 트렌딩 스코어 관리 및 검색 결과 정렬 → RDB 접근 빈도 절약

### 마크다운 지원

- EasyMDE 기반의 마크다운 에디터(이미지 업로드 기능 제공) → WYSIWYG 에디팅 환경 구현
- Markdown-it 기반의 마크다운 렌더러 → anchor, safe-link, 하이라이팅, sanitize 플러그인 구현

### 인증 및 인가

- Access Token & Refresh Token 전략 사용 → JWT 형식으로 Stateless한 인증 및 인가 구현
- OTP 기반의 인증 시스템 구현 → Password-less 인증 시스템 구현
- Redis에 저장된 Refresh Token에 Grace period를 설정 → 토큰 분실 방지

### 기타

- LLM 기반의 질문 답변 봇 → 대기 큐 사용, 쿨다운 처리, 거절 사유(스팸 등)가 있는 경우 예외 처리
- Cloudflare R2(S3 호환) 기반의 이미지 업로드 → 요금 절약(egress 요금 완전 무료)
- PRNG 기반의 좌우대칭 픽셀 패턴 아바타 생성 → GitHub-like 기본 아바타 생성(seed를 통한 고유 아바타)
