# 포유건축 (For You Architecture) - 건축가 포트폴리오 및 상담 관리 시스템

## 프로젝트 개요
건축가 장태성의 전문 포트폴리오 웹사이트로, 30년 경력의 건축 프로젝트를 고급 매거진 스타일(Architectural Digest)로 전시합니다.
실시간 건축상담 요청 관리 및 알림 시스템을 포함합니다. (꽃 상점 기능 제거됨)

## 연락 정보
- 이름: 장태성 (Jang Tae-seong)
- 회사: 포유건축 (For You Architecture)
- 전화: 010-6514-8000
- 이메일: 4upia@naver.com
- 주소: 제주자치도 서귀포시 대정읍 영락하동로 93

## 최근 진행 상황 (2025-12-01 업데이트)

### ✅ 완료된 기능
1. **이원화된 관리 시스템 (문의 + 예약)**
   - 📋 **문의 탭**: 일반 상담 요청 관리
   - 📅 **예약 탭**: 온라인 예약 관리
   - 각각 독립적인 필터링, 통계, 실시간 알림

2. **📱 Web Push 알림 시스템** (2025-12-01 NEW!)
   - 모바일/PC 브라우저에서 푸시 알림 수신
   - 소리 + 진동 지원 (모바일)
   - 무료! (Web Push API 기반)
   - Admin 페이지에서 "📱 모바일 푸시 알림 받기" 버튼 클릭으로 구독
   - 상담 문의 제출 시 자동으로 푸시 알림 전송
   - 테스트 푸시 버튼 제공
   - Service Worker: `/sw.js`
   - VAPID 키: 환경변수로 설정됨

3. **🔔 실시간 알림 배지** (메인 페이지 Hero 섹션) - WebSocket 기반 (2025-12-01 업데이트)
   - 메인 이미지 하단의 공유/복사 버튼 옆에 표시
   - **상담 문의만 카운트** (예약, 후기는 카운트 안 함)
   - 카운터 표시: 🔔 (1), 🔔 (2) 형식
   - 누적 카운팅: 계속 증가 (문의 완료해도 감소 안 함)
   - 링크 없음 (보안 목적)
   - 숨겨진 WebSocket 연결 (NotificationBadgeGlobal)로 모든 페이지에서 안정적인 연결 유지
   - **Admin 페이지에서 초기화 가능** (우측 상단 "🔔 카운터 초기화" 버튼)
   - **PC/모바일 모두 작동** (모바일 터치 이벤트 처리)
   - **반응형**: 모바일에서 버튼 텍스트 숨김, 아이콘만 표시

4. **관리 페이지 실시간 알림** - WebSocket 기반
   - 관리 페이지(/admin)를 열어두면 새로운 상담/예약 요청이 실시간으로 팝업 알림으로 표시
   - 문의와 예약을 구분해서 알림 (다른 아이콘, 메시지)
   - 프리미엄 UI: 녹색 배경, 울리는 벨 아이콘 애니메이션

5. **문의 관리 시스템**
   - 자동 순번 할당 (1, 2, 3... 제출 순서대로)
   - 상담 상태 추적 (완료/미상담)
   - 상담 메모 필드
   - 상담 날짜 자동 기록
   - 다중 필터링: 상태, 날짜 범위, 이름, 전화번호
   - 이메일은 선택사항 (없어도 제출 가능)

6. **온라인 예약 시스템**
   - 날짜, 시간, 상담 유형 선택 (신축/리모델링/인테리어/기타)
   - 자동 순번 할당
   - 완료 상태 추적
   - 예약 메모 필드
   - 다중 필터링: 상태, 날짜 범위, 예약자 이름, 연락처

7. **문의 제출 시스템**
   - 깔끔한 폼 UI
   - "건축상담 요청하기" 브랜딩
   - 이메일 필드는 선택사항

8. **상담 후기 시스템** (2025-11-26)
   - 고객 후기 표시 (5단계 별점, 고객명, 프로젝트 유형)
   - 관리자 페이지에서 후기 추가/수정/삭제 가능
   - 공개/비공개 상태 관리

9. **상담 예약 확인 페이지** (2025-11-26)
   - 고객 전용 예약 조회 시스템
   - 연락처 + 이름으로 자신의 예약 검색
   - 예약 완료 여부 실시간 확인

### ⏳ 구현되었지만 설정 필요
- **이메일 알림** (선택사항)
  - 코드: `server/email.ts`
  - 기능: 새 상담 요청 시 4upia@naver.com으로 HTML 포맷 이메일 발송
  - 현재 상태: NAVER SMTP 인증 설정 이슈로 비활성
  - 추후 설정 시 환경변수 `NAVER_SMTP_PASSWORD` 또는 `GMAIL_APP_PASSWORD` 필요

### ❌ 제거된 기능
- 고부현 플라워 (꽃 상점) - 2025-11-25 완전 제거
  - FlowerShop.tsx 컴포넌트 제거 ✅
  - 네비게이션에서 "꽃" 메뉴 제거 ✅
  - shared/schema.ts에서 flowers, flowerOrders 테이블 정의 제거 ✅
  - server/storage.ts에서 꽃 관련 메서드 제거 ✅
  - server/routes.ts에서 꽃 관련 API 엔드포인트 제거 ✅
  - PostgreSQL 데이터베이스 테이블 삭제 ✅

## 기술 스택
- **Frontend**: React, TypeScript, Tailwind CSS, Framer Motion, Wouter (라우팅)
- **Backend**: Express.js, WebSocket (ws), Multer (파일 업로드)
- **Database**: PostgreSQL (Drizzle ORM)
- **데이터 저장**: PostgreSQL (프로덕션)

## 주요 파일 구조
```
/client
  /src
    /pages
      - Home.tsx: 메인 페이지
      - Admin.tsx: 관리자 대시보드 (문의/예약 탭, 필터링, 실시간 알림)
      - ContactForm.tsx: 건축상담 신청 폼
      - Resume.tsx: 이력서 페이지
      - BookingConfirmation.tsx: 온라인 예약 확인 페이지
      - ReviewsPage.tsx: 상담 후기 페이지
      - ReviewSubmission.tsx: 후기 제출 페이지
    /components
      - Navigation.tsx: 네비게이션
      - Hero.tsx: 메인 이미지 + 알림 배지 + 공유 버튼 (모바일 반응형)
      - NotificationBadge.tsx: 알림 배지 (상담 문의만 표시)
      - NotificationBadgeGlobal.tsx: 숨겨진 전역 WebSocket 연결 (모든 페이지)
      - ShareButtons.tsx: 공유/복사 버튼 (모바일 반응형)
      - PushNotification.tsx: Web Push 알림 구독 UI (Admin 페이지에서 사용)
    - App.tsx: 라우팅 설정

/client/public
  - sw.js: Service Worker (Web Push 알림 수신)

/server
  - routes.ts: API 엔드포인트
  - storage.ts: PostgreSQL ORM 구현 (Drizzle)
  - email.ts: 이메일 발송 유틸리티 (nodemailer)
  - app.ts: Express 앱 설정
  - index-dev.ts: 개발 서버 진입점
  - index-prod.ts: 프로덕션 서버 진입점

/shared
  - schema.ts: Drizzle ORM 스키마
```

## 알림 배지 메커니즘 (2025-12-01 업데이트)

### Architecture
1. **NotificationBadgeGlobal** (App.tsx에서 전역 렌더링)
   - 모든 페이지에서 WebSocket 연결 유지
   - `new_inquiry` 이벤트만 처리
   - localStorage에 inquiryCount 저장
   - `return null` - 시각적으로 렌더링되지 않음

2. **NotificationBadge** (Hero.tsx의 복사 버튼 옆)
   - localStorage에서 inquiryCount 읽음
   - 상담 문의가 있을 때만 렌더링
   - inquiryCount === 0이면 return null

3. **Hero.tsx** (부모 컴포넌트)
   - inquiryCount를 직접 관리
   - `{inquiryCount > 0 && <NotificationBadge />}` 조건부 렌더링
   - visibilitychange 이벤트로 모바일 탭 전환 감지
   - setInterval(500ms)로 주기적 상태 확인

### Flow
```
고객이 상담 문의 제출
         ↓
서버에서 WebSocket으로 "new_inquiry" 메시지 브로드캐스트
         ↓
NotificationBadgeGlobal이 메시지 수신
         ↓
localStorage에 inquiryCount 저장 + inquiryCountChanged 이벤트 발생
         ↓
Hero & NotificationBadge가 이벤트 수신
         ↓
화면에 🔔 (1) 배지 표시

Admin 카운터 초기화 클릭
         ↓
localStorage.removeItem("inquiryCount")
         ↓
inquiryCountChanged 이벤트 발생 (모바일: onTouchEnd로 버튼 작동)
         ↓
Hero & NotificationBadge에서 상태 업데이트
         ↓
배지 사라짐 ✅ (PC/모바일 모두)
```

## 사용 방법

### 고객 관점
1. 메인 페이지에서 복사/공유 버튼 옆 🔔 알림 배지 확인
2. 상담 문의 제출 시 카운터 실시간 증가 확인

### 관리자 관점
1. `/admin` 페이지 접속 (항상 열어둠)
2. 새로운 상담 요청이 실시간으로 팝업 알림으로 표시
3. 알림에서 고객 정보 (이름, 연락처, 이메일) 확인
4. 모바일/PC 모두 "🔔 카운터 초기화" 버튼으로 알림 카운트 초기화
5. 관리 페이지에서 상담 상태, 메모 관리

## 개발 가이드라인
- 모든 interactive 요소와 데이터 표시 요소에 `data-testid` 속성 추가
- 메타 태그: `og:title`, `og:description` 등 정확히 설정
- 한국어 파일명 처리: Base64 (업로드) / UTF-8 RFC 5987 (다운로드) 인코딩
- 모바일 버튼: onTouchEnd 이벤트 처리로 터치 반응 향상

## 배포
- `npm run dev`: 개발 서버 실행 (포트 5000)
- `npm run build`: 프로덕션 빌드

## 최근 버그 수정 및 개선 (2025-12-01)
- ✅ 알림 배지 위치: 메인 Hero 섹션 공유/복사 버튼 옆으로 이동
- ✅ 알림 카운터 반응: localStorage + CustomEvent로 모든 페이지에서 실시간 업데이트
- ✅ NotificationBadgeGlobal: 숨겨진 WebSocket 연결로 안정적인 수신
- ✅ 보안: 알림 배지에 /admin 링크 완전 제거
- ✅ 브라우저 캐시: 최신 코드 로드 확인
- ✅ 카운터 초기화 기능: Admin 페이지 우측 상단에 초기화 버튼 추가
- ✅ **모바일 반응형 최적화** (2025-12-01)
  - 버튼 크기: px-3 py-2 (모바일) → sm:px-4 sm:py-2 (데스크톱)
  - 텍스트 표시: 모바일에서 숨김 → 데스크톱에서 표시
  - 아이콘 크기: w-4 h-4 (모바일) → sm:w-5 sm:h-5
  - **모바일 터치 이벤트**: onTouchEnd로 Admin 초기화 버튼 작동성 확보
  - **상담 문의만 카운트**: 예약/후기는 배지에 미포함
  - **페이지 전환 감지**: visibilitychange + setInterval로 모바일 상태 업데이트

## 향후 개선사항
- Gmail/다른 SMTP 설정으로 이메일 알림 완성
- SMS 알림 (Twilio 또는 다른 서비스)
- 네이버톡톡 메신저 알림
- 예약 확인 페이지 비밀번호/인증 추가 (보안 강화)
