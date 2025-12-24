<div align="center">

# MZC Cloud Native 2기 - TEAM 2

### On-Premise LMS Platform

**대학교 학습 관리 시스템 (Learning Management System)**

[![Project Period](https://img.shields.io/badge/Period-2024.12.04_~_12.24-blue?style=for-the-badge)](.)
[![Team Size](https://img.shields.io/badge/Team-3_Developers-green?style=for-the-badge)](.)

---

<img src="https://raw.githubusercontent.com/MZC-TEAM2/.github/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/%EC%95%84%ED%82%A4%ED%83%9D%EC%B3%90%20%EA%B0%80%EC%9D%B4%EB%93%9C%20%EB%AC%B8%EC%84%9C/%EC%95%84%ED%82%A4%ED%83%9D%EC%B3%90%20%EA%B7%B8%EB%A6%BC.png" alt="Architecture" width="700"/>

</div>

---

## Overview

온프레미스 환경에서 동작하는 대학교 LMS 플랫폼입니다.
**수강신청**, **동영상 강의**, **과제/시험**, **성적 관리** 등 대학 교육에 필요한 핵심 기능을 제공합니다.

<br/>

## Tech Stack

<div align="center">

### Backend
![Java](https://img.shields.io/badge/Java_21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.5-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![JPA](https://img.shields.io/badge/JPA/Hibernate-59666C?style=for-the-badge&logo=hibernate&logoColor=white)

### Database & Cache
![MySQL](https://img.shields.io/badge/MySQL_8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis_7-DC382D?style=for-the-badge&logo=redis&logoColor=white)

### Frontend
![React](https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite_7-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![MUI](https://img.shields.io/badge/MUI_7-007FFF?style=for-the-badge&logo=mui&logoColor=white)

### Infrastructure
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

</div>

<br/>

## Features

<table>
<tr>
<td width="50%">

### 학생
- 수강신청 (장바구니, 시간표 충돌 검사)
- 동영상 강의 시청 (진도율 자동 저장)
- 과제 제출 / 시험 응시
- 성적 조회 / 성적표 PDF 다운로드
- 게시판 / 메시지

</td>
<td width="50%">

### 교수
- 강의 개설 / 주차별 커리큘럼 관리
- 동영상 업로드 (TUS 프로토콜)
- 과제 출제 / 채점
- 시험 출제 (객관식, 주관식)
- 성적 산출 / 공개
- 출석 관리

</td>
</tr>
</table>

<br/>

## Architecture Highlights

| 기술 | 설명 |
|------|------|
| **JWT + Refresh Token** | Access/Refresh 토큰 기반 인증, 자동 갱신 |
| **분산 락 (Redisson)** | 수강신청 동시성 제어, 정원 초과 방지 |
| **TUS Protocol** | 대용량 영상 Resumable Upload |
| **Range Streaming** | HTTP Range 기반 영상 스트리밍 |
| **SSE (Server-Sent Events)** | 실시간 알림 푸시 |
| **부정 시청 감지** | 스킵, 배속, 탭 숨김 감지 |

<br/>

## Repositories

<div align="center">

| Repository | Description | Stack |
|:----------:|:------------|:-----:|
| [**BackEnd_Repository**](https://github.com/MZC-TEAM2/BackEnd_Repository) | LMS 메인 API 서버 | Spring Boot |
| [**Backend_Video_Service_Server**](https://github.com/MZC-TEAM2/Backend_Video_Service_Server) | 비디오 스트리밍 서버 | Spring Boot |
| [**FrontEnd_Repository**](https://github.com/MZC-TEAM2/FrontEnd_Repository) | 웹 클라이언트 | React 19 |

</div>

<br/>

## Documentation

<div align="center">

| 문서 | 설명 |
|:----:|:-----|
| [기능 정의서](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/%EA%B8%B0%EB%8A%A5%20%EC%A0%95%EC%9D%98%EC%84%9C) | 전체 기능 명세 |
| [API 스펙 가이드](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/API%20%EC%8A%A4%ED%8E%99%EA%B0%80%EC%9D%B4%EB%93%9C%20%EB%AC%B8%EC%84%9C) | REST API 명세서 |
| [DB 스키마 가이드](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/DB%20%EC%8A%A4%ED%82%A4%EB%A7%88%20%EA%B0%80%EC%9D%B4%EB%93%9C) | ERD 및 테이블 스펙 |
| [아키텍처 가이드](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/%EC%95%84%ED%82%A4%ED%83%9D%EC%B3%90%20%EA%B0%80%EC%9D%B4%EB%93%9C%20%EB%AC%B8%EC%84%9C) | 시스템 아키텍처 설계 |
| [도메인별 플로우차트](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/%EA%B0%81%20%EB%8F%84%EB%A9%94%EC%9D%B8%EB%B3%84%20%ED%94%8C%EB%A1%9C%EC%9A%B0%EC%B0%A8%ED%8A%B8) | 비즈니스 로직 흐름도 |
| [화면설계서](https://github.com/MZC-TEAM2/.github/tree/main/MZC_TEMA2_%EB%AC%B8%EC%84%9C/%ED%99%94%EB%A9%B4%EC%84%A4%EA%B3%84%EC%84%9C) | UI/UX 설계 |

</div>

<br/>

---

<div align="center">

**MZC Cloud Native 2기 - TEAM 2**

</div>
