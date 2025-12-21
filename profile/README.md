  # On-Premise LMS Platform

  온프레미스 환경의 대학교 학습 관리 시스템

  ## Project Info

  **기간**: 2024.12.04 ~ 2024.12.24 (3주)

  **팀 구성**: Full-Stack 개발 3명

  ---

  ## Architecture

  ┌─────────────────────────────────────────────────────────────────────────────┐
  │                              Client (React)                                  │
  └─────────────────────────────────┬───────────────────────────────────────────┘
                                    │
                                    ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │                            Nginx (Reverse Proxy)                             │
  │               • 정적 파일 서빙  • API 라우팅  • Gzip 압축                       │
  └───────────────────┬─────────────────────────────────┬───────────────────────┘
                      │                                 │
                      ▼                                 ▼
  ┌─────────────────────────────────┐   ┌─────────────────────────────────────┐
  │       LMS API Server            │   │       Video Service Server          │
  │       (Spring Boot)             │   │       (Spring Boot)                 │
  │  • 인증/인가 (JWT)               │   │  • TUS 프로토콜 업로드               │
  │  • 수강신청 (분산 락)             │   │  • HTTP Range 스트리밍              │
  │  • 게시판/메시지                  │   │  • 부정 시청 감지                    │
  │  • 알림 (SSE)                   │   │  • 학습 진도 추적                    │
  └───────────────────┬─────────────┘   └───────────────────┬─────────────────┘
                      │                                     │
                      ▼                                     ▼
            ┌─────────────────┐                   ┌─────────────────┐
            │    MySQL 8.0   │                   │    Redis 7      │
            └─────────────────┘                   └─────────────────┘

  ---

  ## Features

  | 기능 | 설명 |
  |------|------|
  | 강의 관리 | 강의 개설, 주차별 커리큘럼, 자료 업로드 |
  | 수강 신청 | 강의 검색, 장바구니, 일괄 신청 (분산 락) |
  | 동영상 강의 | TUS 업로드, Range 스트리밍, 진도 추적 |
  | 부정 시청 감지 | 스킵/배속/탭 숨김 감지 |
  | 과제 관리 | 과제 출제/제출, 채점 |
  | 출석 관리 | 출석 체크, 출석 현황 조회 |
  | 게시판 | 공지, 자유, Q&A 게시판 |
  | 메시지 | 1:1 대화, 읽음 처리 |
  | 알림 | 실시간 알림 (SSE), 알림 관리 |

  ---

  ## Tech Stack

  ### Backend
  ![Java](https://img.shields.io/badge/Java_21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
  ![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.5-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL_8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
  ![Redis](https://img.shields.io/badge/Redis_7-DC382D?style=for-the-badge&logo=redis&logoColor=white)

  ### Frontend
  ![React](https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black)
  ![Vite](https://img.shields.io/badge/Vite_7-646CFF?style=for-the-badge&logo=vite&logoColor=white)
  ![MUI](https://img.shields.io/badge/MUI_7-007FFF?style=for-the-badge&logo=mui&logoColor=white)
  ![Redux](https://img.shields.io/badge/Redux_Toolkit-764ABC?style=for-the-badge&logo=redux&logoColor=white)

  ### Infrastructure
  ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
  ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

  ---

  ## Repositories

  | Repository | Description |
  |------------|-------------|
  | [BackEnd_Repository](https://github.com/MZC-TEAM2/BackEnd_Repository) | LMS API 서버 (Spring Boot) |
  | [Backend_Video_Service_Server](https://github.com/MZC-TEAM2/Backend_Video_Service_Server) | 비디오 스트리밍 서버 (Spring Boot) |
  | [FrontEnd_Repository](https://github.com/MZC-TEAM2/FrontEnd_Repository) | 웹 클라이언트 (React) |
