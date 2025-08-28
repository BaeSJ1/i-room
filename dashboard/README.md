# Dashboard Service

> i-room 프로젝트의 통합 대시보드 및 관리 서비스

> 목차
> - [📄 서비스 소개](#서비스-소개)
> - [🧑‍💻 개발자](#개발자)
> - [💻 서비스 개발 주안점](#서비스-개발-주안점)
> - [🚀 시작 가이드](#시작-가이드)
> - [⚙️ 기술 스택](#기술-스택)
> - [🏗️ 아키텍처](#아키텍처)
> - [📋 주요 기능](#주요-기능)
> - [🌐 환경별 설정](#환경별-설정)
> - [📡 API 명세](#api-명세)

<a id="서비스-소개"></a>

## 📄 서비스 소개

i-room 서비스의 종합 관리 기능을 담당하는 마이크로서비스입니다. 대시보드 데이터 제공, 도면 관리, 위험구역 설정, PDF 문서 처리, AI 기반 챗봇, 리포트 생성 등 다양한 관리 기능을 통합하여 제공합니다.

### 핵심 기능

- **대시보드**: 현장 안전 지표 및 실시간 모니터링 데이터 제공
- **도면 관리**: 건설 현장 도면 업로드, 조회, 관리 기능
- **위험구역 관리**: 현장 내 위험구역 설정 및 관리
- **AI 문서 처리**: OpenAI 기반 PDF 분석 및 챗봇 서비스
- **리포트 생성**: 안전 관련 리포트 생성 및 관리

<a id="개발자"></a>

## 🧑‍💻 개발자

|             | 이성훈                                                      | 조승빈                                                         | 배소정                                                   |
|-------------|----------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------|
| **E-Mail**  | p.plue1881@gmail.com                                     | benscience@naver.com                                        | bsj9278@gmail.com                                     |
| **GitHub**  | [NextrPlue](https://github.com/NextrPlue)                | [changeme4585](https://github.com/changeme4585)             | [BaeSJ1](https://github.com/BaeSJ1)                   |
| **Profile** | <img src="https://github.com/NextrPlue.png" width=100px> | <img src="https://github.com/changeme4585.png" width=100px> | <img src="https://github.com/BaeSJ1.png" width=100px> |

<a id="서비스-개발-주안점"></a>

## 💻 서비스 개발 주안점

### 📌 AI 통합 관리 시스템

> OpenAI API와 Qdrant 벡터 데이터베이스를 활용한 지능형 문서 처리 시스템을 구축했습니다.
>
> PDF 문서의 임베딩 생성, 벡터 검색, 번역 서비스를 통해 현장 관리자가 안전 매뉴얼을 효율적으로 활용할 수 있도록 했습니다.

### 📌 벡터 디비 구축

> 산업 안전 지침서를 영어로 번역 후 임베딩하여 저장하고, 유사도 검색을 통해 필요한 정보를 빠르게 탐색합니다.
>
> 이를 통해 LLM 프롬프트에 맥락을 보강하여 정확성을 높였습니다.

### 📌 LLM을 통한 리포트 생성

> GPT API를 활용해 날짜별 산업 안전 지표 기반 리포트를 자동 생성합니다.
>
> 프롬프트 최적화를 통해 응답 품질을 개선하고, 현장 관리자에게 이해하기 쉬운 형태로 전달합니다.

<a id="시작-가이드"></a>

## 🚀 시작 가이드

### 사전 준비 사항

- Java 17
- Gradle 8.14 이상

### 서비스 실행

1. **프로젝트 클론 및 디렉토리 이동**
   ```bash
   git clone {저장소 URL}
   cd i-room/dashboard
   ```

2. **Gradle을 사용하여 애플리케이션 실행**
   ```bash
   ./gradlew bootRun
   ```
   *Windows의 경우:*
   ```bash
   gradlew.bat bootRun
   ```

3. **데이터베이스 설정** (필수)
   MySQL 데이터베이스가 실행 중이어야 하며, `iroom_dashboard` 데이터베이스가 생성되어 있어야 합니다.
   ```sql
   CREATE DATABASE iroom_dashboard;
   ```

4. **외부 서비스 설정** (필수)
   ```bash
   # 환경변수 설정
   export OPENAI_API_KEY=your-openai-api-key
   export TRANSLATE_AUTH_KEY=your-translation-api-key
   ```
    - Kafka: `localhost:9092`
    - Qdrant: `localhost:6333`

5. **애플리케이션 접속**
   서비스가 정상적으로 실행되면 `http://localhost:8085`에서 서비스가 활성화됩니다.

<a id="기술-스택"></a>

## ⚙️ 기술 스택

- **Java 17**: 프로그래밍 언어
- **Spring Boot 3.5.3**: 애플리케이션 프레임워크
- **Spring Data JPA**: 데이터베이스 ORM
- **Spring Cloud 2025.0.0**: 마이크로서비스 인프라
- **Spring Cloud Stream**: Kafka 메시징
- **Spring Cloud OpenFeign**: 선언적 REST 클라이언트
- **MySQL 8.0**: 관계형 데이터베이스
- **Qdrant**: 벡터 데이터베이스 (문서 임베딩)
- **Apache Kafka**: 이벤트 스트리밍
- **OpenAI API**: GPT-4o, DALL-E 3 AI 서비스
- **iTextPDF & PDFBox**: PDF 문서 처리
- **Gradle**: 빌드 도구
- **Micrometer**: 메트릭 및 추적

<a id="아키텍처"></a>

## 🏗️ 아키텍처

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│     Gateway     │    │   Dashboard     │    │    MySQL DB     │
│                 │◄──►│   Service       │◄──►│   (iroom_       │
│  - JWT Auth     │    │                 │    │   dashboard)    │
│  - Routing      │    │ - Dashboard     │    │                 │
└─────────────────┘    │ - Blueprint     │    │ - dashboards    │
                       │ - DangerArea    │    │ - blueprints    │
                       │ - PDF/AI Chat   │    │ - danger_areas  │
                       │ - Reports       │    │ - reports       │
                       └─────────────────┘    │ - incidents     │
                             ▲  ▲  ▲          └─────────────────┘
               ┌─────────────┘  │  └──────────────┐
               ▼                ▼                 ▼
    ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
    │   Qdrant DB     │ │   Kafka Broker  │ │   OpenAI API    │
    │                 │ │                 │ │                 │
    │ - PDF Vectors   │ │  Topic: iroom   │ │  - GPT-4o       │
    │ - Embeddings    │ │ - AlarmEvent    │ │  - DALL-E 3     │
    │ - Similarity    │ │ - WorkerEvent   │ │  - Embeddings   │
    └─────────────────┘ └─────────────────┘ └─────────────────┘
                                ▲
                                │
                                ▼
                    ┌────────────────────────┐
                    │     Other Services     │
                    └────────────────────────┘
```

<a id="주요-기능"></a>

## 📋 주요 기능

### 1. 대시보드 관리 (`/dashboards/**`)

- **메트릭 조회**: `GET /dashboards/metrics/{interval}` (일/주/월별 통계)
- **대시보드 데이터**: 현장 안전 지표 및 실시간 모니터링
- **사고 현황**: 위험 감지 및 사고 통계

### 2. 도면 관리 (`/blueprints/**`)

- **도면 등록**: `POST /blueprints` (멀티파트 파일 업로드)
- **도면 조회**: `GET /blueprints/{blueprintId}`
- **도면 목록**: `GET /blueprints` (페이징)
- **도면 수정**: `PUT /blueprints/{blueprintId}`
- **도면 삭제**: `DELETE /blueprints/{blueprintId}`

### 3. 위험구역 관리 (`/danger-areas/**`)

- **위험구역 생성**: `POST /danger-areas`
- **위험구역 조회**: `GET /danger-areas/{dangerAreaId}`
- **위험구역 목록**: `GET /danger-areas/blueprint/{blueprintId}`
- **위험구역 수정**: `PUT /danger-areas/{dangerAreaId}`
- **위험구역 삭제**: `DELETE /danger-areas/{dangerAreaId}`

### 4. AI 문서 처리 (`/upload-pdf`, `/chat/**`)

- **PDF 업로드**: `POST /upload-pdf` (PDF 문서 임베딩)
- **AI 챗봇**: `POST /chat` (문서 기반 질의응답)
- **번역 서비스**: 다국어 지원
- **벡터 검색**: Qdrant를 통한 유사도 검색

### 5. 리포트 관리 (`/reports/**`)

- **리포트 생성**: `POST /reports`
- **리포트 조회**: `GET /reports/{reportId}`
- **리포트 목록**: `GET /reports` (페이징)

<a id="환경별-설정"></a>

## 🌐 환경별 설정

### 로컬 개발 환경 (기본)

- **Database**: `localhost:3306/iroom_dashboard`
- **Kafka**: `localhost:9092`
- **Qdrant**: `localhost:6333`
- **OpenAI API**: 환경변수 `OPENAI_API_KEY` 필요
- **Translation API**: 환경변수 `TRANSLATE_AUTH_KEY` 필요

### Docker 환경 (`docker` 프로필)

- **Database**: `mysql:3306/iroom_dashboard`
- **Kafka**: `kafka:9093`

### Kubernetes 환경 (`k8s` 프로필)

- **Database**: `i-room-mysql/iroom_dashboard`
- **Kafka**: `i-room-kafka:9092`
- **Qdrant**: `i-room-qdrant:6333`

<a id="api-명세"></a>

## 📡 API 명세

대시보드 서비스 관련 API 명세는 아래 링크의 'Dashboard' 섹션에서 확인할 수 있습니다.

- [i-room API 명세서 (Notion)](https://disco-mitten-e75.notion.site/API-238f6cd45c7380209227f1f66bddebdd?pvs=73)
