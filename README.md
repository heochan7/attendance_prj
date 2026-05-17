# 📌 Attendance Project (출석 관리 시스템)

스프링 부트(Spring Boot) 백엔드와 리액트(React + TypeScript) 프론트엔드를 하나의 저장소에서 관리하는 모노레포(Monorepo) 기반의 출석 관리 시스템 프로젝트입니다.

---

## 🏗️ 프로젝트 구조 (Project Architecture)

최상위 디렉터리에서 백엔드와 프론트엔드가 독립된 모듈로 나란히 관리되며, 깃허브 데스크톱(GitHub Desktop)을 통해 통합 버전 관리가 이루어집니다.

```
attendance_prj/ (★ 루트 저장소 - 통합 Git 관리)
├── README.md
├── .gitignore
├── attendance_backend/    (Backend: Spring Boot 3.x)
│   ├── src/
│   └── build.gradle
└── attendance_frontend/   (Frontend: React + TypeScript + Vite)
    ├── src/
    └── package.json
```

---

## 🛠️ 기술 스택 (Tech Stack)

### Backend
* **Framework:** Spring Boot 3.x
* **Database:** H2 (Local Dev) / PostgreSQL (Production)
* **ORM:** Spring Data JPA
* **Build Tool:** Gradle

### Frontend
* **Library:** React 18+
* **Language:** TypeScript
* **Build Tool:** Vite
* **HTTP Client:** Axios

---

## 🚀 시작하기 (Getting Started)

### 1. Prerequisites
프로젝트를 실행하기 위해 로컬 컴퓨터에 아래 개발 환경이 설치되어 있어야 합니다.
* **Java** 17 또는 21
* **Node.js** LTS 버전 (v20 이상 권장)

### 2. Backend 실행 방법
1. IntelliJ IDEA에서 `attendance_backend` 폴더를 엽니다.
2. `src/main/java/.../*Application.java` 파일을 실행하거나 터미널에서 아래 명령어를 입력합니다.
```bash
cd attendance_backend
./gradlew bootRun
```
* **Local DB Profile:** 기본적으로 메모리 기반의 **H2 DB**가 활성화됩니다.
* **Production Profile:** 배포 환경(`prod`)에서는 외부 환경 변수(`SPRING_DATASOURCE_URL` 등)를 주입받아 **PostgreSQL**과 연동됩니다.

### 3. Frontend 실행 방법
1. 터미널을 열고 프론트엔드 디렉터리로 이동 후 패키지를 설치합니다.
```bash
cd attendance_frontend
npm install
```
2. 로컬 개발 서버를 구동합니다. (IntelliJ 우측 상단의 `npm` 실행 구성을 활용하면 마우스 클릭으로 편리하게 구동할 수 있습니다.)
```bash
npm run dev
```
* 기본 로컬 접속 주소: `http://localhost:5173/`

---

## ⚙️ 환경 설정 및 배포 유의사항 (Configuration)

### 데이터베이스 프로필 관리 (`application-prod.yml`)
운영 배포 환경에서는 보안 및 최적화를 위해 데이터베이스 접속 정보를 환경 변수로 주입받습니다. 드라이버 클래스 네임(`driver-class-name`)은 주입되는 JDBC URL 주소(`jdbc:postgresql://...`)를 바탕으로 스프링 부트가 자동 매핑하도록 최적화되어 있습니다.

```yaml
spring:
  datasource:
    url: ${SPRING_DATASOURCE_URL}
    username: ${SPRING_DATASOURCE_USERNAME}
    password: ${SPRING_DATASOURCE_PASSWORD}
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

### Git 버전 관리 규칙
* 본 프로젝트는 루트의 `attendance_prj`에서만 `.git` 저장소를 생성하여 하위 모듈을 통합 관리합니다.
* 각 하위 폴더 생성 시 자동으로 만들어지는 개별 숨김 `.git` 폴더는 충돌 방지를 위해 모두 자식 디렉터리에서 제거된 상태를 유지해야 합니다.
