# Seoul Shadow Map - 서울시 3D 그림자 시각화 앱

## 프로젝트 개요
서울시 지도에 건물의 3D 구조를 시각화하고, 실시간으로 그림자가 드리워진 지역을 표현하는 웹 애플리케이션입니다. 사용자는 시간대별 그림자 변화를 확인하고, 특정 위치의 일조량 정보를 분석할 수 있습니다.

## 핵심 기능
- 서울시 3D 건물 지도 렌더링
- 실시간/시간대별 그림자 시뮬레이션
- 일조량 분석 및 시각화
- 위치 기반 그림자 정보 제공

## Claude Code 개발 철칙

### 1. 코드 품질 원칙
- **Clean Code**: 읽기 쉽고 이해하기 쉬운 코드 작성
- **SOLID 원칙**: 객체지향 설계 원칙 준수
- **DRY (Don't Repeat Yourself)**: 코드 중복 최소화
- **YAGNI (You Aren't Gonna Need It)**: 필요한 기능만 구현
- **단일 책임 원칙**: 하나의 함수/클래스는 하나의 책임만

### 2. 개발 표준
```typescript
// 파일 네이밍 컨벤션
components/ShadowMap.tsx
utils/geometryCalculator.ts
types/BuildingData.ts
services/shadowApi.ts

// 변수 및 함수 네이밍
const buildingHeight = 45.6;
const calculateShadowArea = () => {};
const getUserLocation = async () => {};

// 상수는 대문자로
const MAX_BUILDING_HEIGHT = 1000;
const API_ENDPOINTS = {
  BUILDINGS: '/api/buildings',
  SHADOW_DATA: '/api/shadows'
};
```

### 3. 아키텍처 패턴
- **Component-Based Architecture**: React 컴포넌트 기반 설계
- **Service Layer Pattern**: 비즈니스 로직 분리
- **Repository Pattern**: 데이터 접근 계층 추상화
- **Observer Pattern**: 상태 변화 감지 및 반응

### 4. 성능 최적화
- 3D 렌더링 최적화 (LOD, Frustum Culling)
- 메모리 관리 (텍스처, 지오메트리 해제)
- 비동기 데이터 로딩
- 캐싱 전략 구현

## GIT 관리 전략

### Branch 전략
```
main (운영)
├── develop (개발)
├── feature/shadow-calculation (기능 개발)
├── feature/3d-building-render (기능 개발)
├── hotfix/critical-bug-fix (긴급 수정)
└── release/v1.0.0 (릴리즈 준비)
```

### Commit 메시지 규칙
```
feat: 새로운 기능 추가
fix: 버그 수정
docs: 문서 수정
style: 코드 포맷팅, 세미콜론 누락 등
refactor: 코드 리팩토링
test: 테스트 추가 또는 수정
chore: 빌드 프로세스 또는 보조 도구 변경

예시:
feat: 3D 건물 렌더링 기능 추가
fix: 그림자 계산 알고리즘 오류 수정
docs: API 문서 업데이트
```

### Code Review 체크리스트
- [ ] 기능 요구사항 충족
- [ ] 코드 가독성 및 주석
- [ ] 성능 최적화 고려
- [ ] 에러 핸들링
- [ ] 테스트 케이스 포함
- [ ] 보안 취약점 검토

## 개발 문서 정리 양식

### 1. 기능 개발 문서 구조
```
📁 docs/
├── 📄 architecture.md (시스템 아키텍처)
├── 📄 api-specification.md (API 명세서)
├── 📄 database-schema.md (데이터베이스 설계)
├── 📄 deployment-guide.md (배포 가이드)
└── 📁 features/
    ├── 📄 3d-rendering.md
    ├── 📄 shadow-calculation.md
    └── 📄 user-interaction.md
```

### 2. 기능 문서 템플릿
```markdown
# [기능명]

## 개요
기능에 대한 간략한 설명

## 요구사항
- 기능적 요구사항 1
- 기능적 요구사항 2
- 비기능적 요구사항

## 기술 설계
### 아키텍처
### 데이터 모델
### API 설계

## 구현 상세
### 핵심 로직
### 최적화 포인트
### 에러 처리

## 테스트 시나리오
### 단위 테스트
### 통합 테스트
### 성능 테스트

## 배포 고려사항
```

### 3. 코드 문서화 규칙
```typescript
/**
 * 건물 그림자를 계산하는 함수
 * @param building 건물 정보 객체
 * @param sunPosition 태양 위치 (위도, 경도, 높이)
 * @param timeOfDay 시간 (ISO 8601 형식)
 * @returns 그림자 폴리곤 좌표 배열
 * @throws {Error} 유효하지 않은 건물 데이터일 경우
 * @example
 * const shadow = calculateBuildingShadow(
 *   { height: 100, coordinates: [...] },
 *   { lat: 37.5665, lng: 126.9780, altitude: 45 },
 *   '2024-06-21T12:00:00Z'
 * );
 */
function calculateBuildingShadow(
  building: BuildingData,
  sunPosition: SunPosition,
  timeOfDay: string
): ShadowPolygon[] {
  // 구현 내용
}
```

## Claude Code 활용 가이드

### 1. 프롬프트 작성 규칙
- 구체적이고 명확한 요구사항 작성
- 예상 입력/출력 데이터 예시 제공
- 에러 처리 및 엣지 케이스 고려사항 명시
- 성능 요구사항 포함

### 2. 코드 리뷰 요청 시
```
이 코드를 리뷰해주세요:
1. 성능 최적화 포인트
2. 보안 취약점
3. 코드 가독성 개선
4. 테스트 케이스 누락
5. 메모리 누수 가능성
```

### 3. 디버깅 지원 요청
```
다음 오류를 해결해주세요:
- 오류 메시지: [구체적인 에러 메시지]
- 발생 상황: [재현 단계]
- 기대 동작: [예상되는 정상 동작]
- 환경 정보: [브라우저, Node.js 버전 등]
```

## 개발 환경 설정

### 필수 도구
- Node.js 18+ 
- TypeScript 5+
- React 18+
- Three.js (3D 렌더링)
- Mapbox GL JS (지도 서비스)
- Vite (빌드 도구)

### 개발 환경 명령어
```bash
# 프로젝트 초기화
npm create vite@latest seoul-shadow-map --template react-ts

# 개발 서버 실행
npm run dev

# 빌드
npm run build

# 테스트 실행
npm run test

# 린팅
npm run lint
```

## 보안 가이드라인

1. **API 보안**: 모든 외부 API 요청에 인증 토큰 사용
2. **데이터 검증**: 사용자 입력 데이터 검증 및 새니타이징
3. **XSS 방지**: 사용자 생성 콘텐츠 이스케이프 처리
4. **HTTPS**: 모든 통신에 HTTPS 사용
5. **민감 정보**: 환경 변수를 통한 설정 관리