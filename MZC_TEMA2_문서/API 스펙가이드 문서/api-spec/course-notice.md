# Course Notice API

> 강의 공지사항 API

## 목차

### 공지사항 관리
- [1. 공지사항 생성 (교수)](#1-공지사항-생성-교수)
- [2. 공지사항 목록 조회](#2-공지사항-목록-조회)
- [3. 공지사항 상세 조회](#3-공지사항-상세-조회)
- [4. 공지사항 수정 (교수)](#4-공지사항-수정-교수)
- [5. 공지사항 삭제 (교수)](#5-공지사항-삭제-교수)

### 댓글 관리
- [6. 댓글 작성](#6-댓글-작성)
- [7. 대댓글 작성](#7-대댓글-작성)
- [8. 댓글 수정](#8-댓글-수정)
- [9. 댓글 삭제](#9-댓글-삭제)

---

## 1. 공지사항 생성 (교수)

강의 공지사항을 생성합니다. 담당 교수만 가능합니다.

### Request
```
POST /api/v1/courses/{courseId}/notices
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Request Body
```json
{
  "title": "중간고사 안내",
  "content": "중간고사는 4월 15일에 진행됩니다.",
  "allowComments": true
}
```

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| title | string | O | 제목 (최대 200자) |
| content | string | O | 내용 |
| allowComments | boolean | O | 댓글 허용 여부 |

### Response
```json
{
  "success": true,
  "data": {
    "id": 1,
    "courseId": 24,
    "title": "중간고사 안내",
    "allowComments": true,
    "authorId": 20250101002,
    "authorName": "김교수",
    "createdAt": "2025-04-01T10:00:00",
    "updatedAt": "2025-04-01T10:00:00"
  },
  "message": "공지사항이 생성되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 400 | INVALID_INPUT | 입력값 유효성 검증 실패 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_OWNER | 담당 교수가 아님 |
| 404 | COURSE_NOT_FOUND | 강의를 찾을 수 없음 |

---

## 2. 공지사항 목록 조회

강의 공지사항 목록을 조회합니다. 수강생 및 담당 교수만 조회 가능합니다.

### Request
```
GET /api/v1/courses/{courseId}/notices
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |

### Query Parameters
| 파라미터 | 타입 | 필수 | 설명 | 기본값 |
|----------|------|------|------|--------|
| page | int | X | 페이지 번호 | 0 |
| size | int | X | 페이지 크기 | 10 |
| sort | string | X | 정렬 기준 | createdAt,desc |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Response
```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "courseId": 24,
        "title": "중간고사 안내",
        "allowComments": true,
        "authorId": 20250101002,
        "authorName": "김교수",
        "createdAt": "2025-04-01T10:00:00",
        "updatedAt": "2025-04-01T10:00:00"
      }
    ],
    "pageable": {
      "pageNumber": 0,
      "pageSize": 10,
      "sort": { "sorted": true, "direction": "DESC" }
    },
    "totalElements": 6,
    "totalPages": 1
  }
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_ENROLLED | 수강생/담당교수가 아님 |
| 404 | COURSE_NOT_FOUND | 강의를 찾을 수 없음 |

---

## 3. 공지사항 상세 조회

강의 공지사항 상세 정보를 조회합니다 (댓글 포함).

### Request
```
GET /api/v1/courses/{courseId}/notices/{noticeId}
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Response
```json
{
  "success": true,
  "data": {
    "id": 1,
    "courseId": 24,
    "title": "중간고사 안내",
    "content": "중간고사는 4월 15일에 진행됩니다.\n\n시험 범위: 1주차~7주차\n준비물: 학생증, 필기구",
    "allowComments": true,
    "authorId": 20250101002,
    "authorName": "김교수",
    "createdAt": "2025-04-01T10:00:00",
    "updatedAt": "2025-04-01T10:00:00",
    "comments": [
      {
        "id": 1,
        "noticeId": 1,
        "parentId": null,
        "content": "시험 범위가 어디까지인가요?",
        "authorId": 20250101012,
        "authorName": "홍길동",
        "createdAt": "2025-04-02T14:30:00",
        "updatedAt": "2025-04-02T14:30:00",
        "children": [
          {
            "id": 2,
            "noticeId": 1,
            "parentId": 1,
            "content": "1주차부터 7주차까지입니다.",
            "authorId": 20250101002,
            "authorName": "김교수",
            "createdAt": "2025-04-02T15:00:00",
            "updatedAt": "2025-04-02T15:00:00",
            "children": []
          }
        ]
      }
    ]
  }
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_ENROLLED | 수강생/담당교수가 아님 |
| 404 | COURSE_NOT_FOUND | 강의를 찾을 수 없음 |
| 404 | NOTICE_NOT_FOUND | 공지사항을 찾을 수 없음 |

---

## 4. 공지사항 수정 (교수)

강의 공지사항을 수정합니다. 담당 교수만 가능합니다.

### Request
```
PUT /api/v1/courses/{courseId}/notices/{noticeId}
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Request Body
```json
{
  "title": "중간고사 안내 (수정)",
  "content": "중간고사가 4월 20일로 연기되었습니다.",
  "allowComments": true
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": 1,
    "courseId": 24,
    "title": "중간고사 안내 (수정)",
    "allowComments": true,
    "authorId": 20250101002,
    "authorName": "김교수",
    "createdAt": "2025-04-01T10:00:00",
    "updatedAt": "2025-04-05T09:00:00"
  },
  "message": "공지사항이 수정되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 400 | INVALID_INPUT | 입력값 유효성 검증 실패 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_OWNER | 담당 교수가 아님 |
| 404 | NOTICE_NOT_FOUND | 공지사항을 찾을 수 없음 |

---

## 5. 공지사항 삭제 (교수)

강의 공지사항을 삭제합니다 (Soft Delete). 담당 교수만 가능합니다.

### Request
```
DELETE /api/v1/courses/{courseId}/notices/{noticeId}
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Response
```json
{
  "success": true,
  "message": "공지사항이 삭제되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_OWNER | 담당 교수가 아님 |
| 404 | NOTICE_NOT_FOUND | 공지사항을 찾을 수 없음 |

---

## 6. 댓글 작성

공지사항에 댓글을 작성합니다. 수강생 및 담당 교수 모두 가능합니다.

### Request
```
POST /api/v1/courses/{courseId}/notices/{noticeId}/comments
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Request Body
```json
{
  "content": "시험 범위가 어디까지인가요?"
}
```

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| content | string | O | 댓글 내용 |

### Response
```json
{
  "success": true,
  "data": {
    "id": 1,
    "noticeId": 1,
    "parentId": null,
    "content": "시험 범위가 어디까지인가요?",
    "authorId": 20250101012,
    "authorName": "홍길동",
    "createdAt": "2025-04-02T14:30:00",
    "updatedAt": "2025-04-02T14:30:00",
    "children": []
  },
  "message": "댓글이 작성되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 400 | INVALID_INPUT | 입력값 유효성 검증 실패 |
| 400 | COMMENTS_NOT_ALLOWED | 댓글이 허용되지 않은 공지 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_ENROLLED | 수강생/담당교수가 아님 |
| 404 | NOTICE_NOT_FOUND | 공지사항을 찾을 수 없음 |

---

## 7. 대댓글 작성

공지사항 댓글에 대댓글을 작성합니다. 최대 2depth까지 지원합니다.

### Request
```
POST /api/v1/courses/{courseId}/notices/{noticeId}/comments/{parentId}/replies
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |
| parentId | long | O | 부모 댓글 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Request Body
```json
{
  "content": "1주차부터 7주차까지입니다."
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": 2,
    "noticeId": 1,
    "parentId": 1,
    "content": "1주차부터 7주차까지입니다.",
    "authorId": 20250101002,
    "authorName": "김교수",
    "createdAt": "2025-04-02T15:00:00",
    "updatedAt": "2025-04-02T15:00:00",
    "children": []
  },
  "message": "답글이 작성되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 400 | INVALID_INPUT | 입력값 유효성 검증 실패 |
| 400 | COMMENTS_NOT_ALLOWED | 댓글이 허용되지 않은 공지 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 404 | COMMENT_NOT_FOUND | 부모 댓글을 찾을 수 없음 |

---

## 8. 댓글 수정

공지사항 댓글을 수정합니다. 작성자만 가능합니다.

### Request
```
PUT /api/v1/courses/{courseId}/notices/{noticeId}/comments/{commentId}
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |
| commentId | long | O | 댓글 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Request Body
```json
{
  "content": "시험 범위가 1~7주차라고 공지에 있네요!"
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": 1,
    "noticeId": 1,
    "parentId": null,
    "content": "시험 범위가 1~7주차라고 공지에 있네요!",
    "authorId": 20250101012,
    "authorName": "홍길동",
    "createdAt": "2025-04-02T14:30:00",
    "updatedAt": "2025-04-02T16:00:00",
    "children": []
  },
  "message": "댓글이 수정되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 400 | INVALID_INPUT | 입력값 유효성 검증 실패 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_AUTHOR | 작성자가 아님 |
| 404 | COMMENT_NOT_FOUND | 댓글을 찾을 수 없음 |

---

## 9. 댓글 삭제

공지사항 댓글을 삭제합니다 (Soft Delete). 작성자만 가능합니다.

### Request
```
DELETE /api/v1/courses/{courseId}/notices/{noticeId}/comments/{commentId}
```

### Path Parameters
| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| courseId | long | O | 강의 ID |
| noticeId | long | O | 공지사항 ID |
| commentId | long | O | 댓글 ID |

### Headers
| 헤더 | 필수 | 설명 |
|------|------|------|
| Authorization | O | Bearer {accessToken} |

### Response
```json
{
  "success": true,
  "message": "댓글이 삭제되었습니다."
}
```

### Error Codes
| HTTP Status | 에러 코드 | 설명 |
|-------------|-----------|------|
| 401 | UNAUTHORIZED | 인증 필요 |
| 403 | NOT_AUTHOR | 작성자가 아님 |
| 404 | COMMENT_NOT_FOUND | 댓글을 찾을 수 없음 |

---

## 데이터 모델

### CourseNoticeResponse
| 필드 | 타입 | 설명 |
|------|------|------|
| id | number | 공지사항 ID |
| courseId | number | 강의 ID |
| title | string | 제목 |
| allowComments | boolean | 댓글 허용 여부 |
| authorId | number | 작성자 ID |
| authorName | string | 작성자 이름 |
| createdAt | datetime | 생성일시 |
| updatedAt | datetime | 수정일시 |

### CourseNoticeDetailResponse
| 필드 | 타입 | 설명 |
|------|------|------|
| id | number | 공지사항 ID |
| courseId | number | 강의 ID |
| title | string | 제목 |
| content | string | 내용 |
| allowComments | boolean | 댓글 허용 여부 |
| authorId | number | 작성자 ID |
| authorName | string | 작성자 이름 |
| createdAt | datetime | 생성일시 |
| updatedAt | datetime | 수정일시 |
| comments | CourseNoticeCommentResponse[] | 댓글 목록 |

### CourseNoticeCommentResponse
| 필드 | 타입 | 설명 |
|------|------|------|
| id | number | 댓글 ID |
| noticeId | number | 공지사항 ID |
| parentId | number \| null | 부모 댓글 ID (대댓글인 경우) |
| content | string | 댓글 내용 |
| authorId | number | 작성자 ID |
| authorName | string | 작성자 이름 |
| createdAt | datetime | 생성일시 |
| updatedAt | datetime | 수정일시 |
| children | CourseNoticeCommentResponse[] | 대댓글 목록 |

---

## 권한 정리

| API | 교수 (담당) | 교수 (비담당) | 학생 (수강) | 학생 (미수강) |
|-----|-------------|---------------|-------------|---------------|
| 공지 생성 | O | X | X | X |
| 공지 조회 | O | X | O | X |
| 공지 수정 | O | X | X | X |
| 공지 삭제 | O | X | X | X |
| 댓글 작성 | O | X | O | X |
| 댓글 수정 | 본인만 | - | 본인만 | - |
| 댓글 삭제 | 본인만 | - | 본인만 | - |

---

**문서 작성일**: 2025-12-23
