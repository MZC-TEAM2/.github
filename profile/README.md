# On-Premise LMS Platform

온프레미스 환경에서 구축하는 학습 관리 시스템

## Project Info

**기간**: 2024.12.04 ~ 2024.12.24 (3주)

**팀 구성**: Full-Stack 개발 3명

## Features

- 강의 관리: 강의 개설, 커리큘럼 구성, 자료 업로드
- 수강 신청: 강의 검색, 수강 신청/취소, 수강 이력
- 과제/시험 관리: 과제 출제/제출, 시험 출제/응시, 채점
- 동영상 강의: 영상 스트리밍, 시청 이력 추적
- 실시간 강의: 화상 강의, 채팅, 출석 체크
- 수강생 관리: 진도율 추적, 성적 관리

## Tech Stack

### Backend
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

### Frontend
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)

### Infrastructure
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

## Repositories

- [Backend Repository](링크) - Spring Boot API Server
- [Frontend Repository](링크) - React Web Application

## API Documentation

Swagger UI를 통해 API 명세를 확인할 수 있습니다.

```
http://localhost:8080/swagger-ui.html
```

## Quick Start

### Backend
```bash
cd backend
./gradlew bootRun
```

### Frontend
```bash
cd frontend
npm install
npm start
```

### Docker
```bash
docker-compose up -d
```

## Development

### Branch Strategy
- `main` - 프로덕션
- `develop` - 개발 통합
- `feature/*` - 기능 개발

### Commit Convention
```
feat: 기능 추가
fix: 버그 수정
docs: 문서 수정
refactor: 리팩토링
```
