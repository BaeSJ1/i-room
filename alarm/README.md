# Alarm Service

> i-room 프로젝트의 실시간 위험 알림 서비스

> 목차
> - [📄 서비스 소개](#서비스-소개)
> - [🧑‍💻 개발자](#개발자)
> - [💻 서비스 개발 주안점](#서비스-개발-주안점)
> - [🚀 시작 가이드](#시작-가이드)
> - [⚙️ 기술 스택](#기술-스택)
> - [📡 API 명세](#api-명세)

<a id="서비스-소개"></a>
## 📄 서비스 소개

Kafka로부터 위험 감지 이벤트를 수신하여, 관리자 및 대시보드에 실시간으로 알림을 전송하는 마이크로서비스입니다.

### 주요 기능

- **위험 이벤트 수신**: Kafka로부터 근로자 위험 감지 이벤트를 구독(Subscribe)합니다.
- **실시간 알림 발송**: SSE(Server-Sent Events)를 통해 웹 브라우저 및 클라이언트로 실시간 알림을 전송합니다.
- **알림 이력 관리**: 발생한 모든 알림을 데이터베이스에 기록하고, 필요시 조회할 수 있는 기능을 제공합니다.

<a id="개발자"></a>
## 🧑‍💻 개발자

|          | 이성훈                                                      | 배소정                                                     |
|----------|-------------------------------------------------------------|------------------------------------------------------------|
| **E-Mail** | p.plue1881@gmail.com                                        | bsj9278@gmail.com                                          |
| **GitHub** | [NextrPlue](https://github.com/NextrPlue)                   | [BaeSJ1](https://github.com/BaeSJ1)                        |
| **Profile**  | <img src="https://github.com/NextrPlue.png" width=100px>    | <img src="https://github.com/BaeSJ1.png" width=100px>      |

<a id="서비스-개발-주안점"></a>
## 💻 서비스 개발 주안점

### 📌 이벤트 기반 실시간 통신
> Kafka를 통해 비동기적으로 이벤트를 수신하고, SSE(Server-Sent Events)를 통해 클라이언트에게 실시간으로 알림을 전파하는 이벤트 기반 아키텍처를 구현했습니다. 이를 통해 시스템 간의 결합도를 낮추고 확장성을 확보했습니다.

<a id="시작-가이드"></a>
## 🚀 시작 가이드

### 사전 준비 사항

- Java 17
- Gradle 8.14 이상

### 서비스 실행

1.  **프로젝트 클론 및 디렉토리 이동**
    ```bash
    git clone {저장소 URL}
    cd i-room/alarm
    ```

2.  **Gradle을 사용하여 애플리케이션 실행**
    ```bash
    ./gradlew bootRun
    ```
    *Windows의 경우:*
    ```bash
    gradlew.bat bootRun
    ```

3.  **애플리케이션 접속**
    서비스가 정상적으로 실행되면 `http://localhost:8084` (또는 application.yml에 설정된 포트)에서 서비스가 활성화되고, 클라이언트는 해당 주소의 SSE 엔드포인트를 구독할 수 있습니다.

<a id="기술-스택"></a>
## ⚙️ 기술 스택

- **Java 17**: 프로그래밍 언어
- **Spring Boot**: 애플리케이션 프레임워크
- **Spring WebFlux**: SSE(Server-Sent Events) 구현
- **Spring for Apache Kafka**: Kafka 연동
- **Spring Data JPA**: 데이터베이스 연동
- **MySQL**: 데이터베이스
- **Gradle**: 빌드 도구

<a id="api-명세"></a>
## 📡 API 명세

알림 서비스는 클라이언트가 구독할 수 있는 SSE(Server-Sent Events) 엔드포인트를 제공합니다. 자세한 내용은 아래 Notion 링크의 'Alarm' 섹션을 참고하십시오.

- [i-room API 명세서 (Notion)](https://disco-mitten-e75.notion.site/API-238f6cd45c7380209227f1f66bddebdd?pvs=73)
