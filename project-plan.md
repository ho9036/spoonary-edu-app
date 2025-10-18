# Spoonary 데스크탑 앱 기획서

## 📋 프로젝트 개요

### 프로젝트명
**Spoonary** - Robot Control System

### 목적
로봇손 제품의 통합 제어 및 관리를 위한 데스크탑 애플리케이션

### 기술 스택
- **프레임워크**: Electron.js
- **UI 라이브러리**: React
- **스타일링**: Tailwind CSS
- **3D 렌더링**: Three.js (시뮬레이터)
- **브랜드 컬러**: #37BBA3 (청록색)

---

## 🎨 디자인 시스템

### 컬러 팔레트
- **Primary Color**: #37BBA3 (청록색)
- **Secondary Color**: Cyan-400 (#22D3EE)
- **Background**: Slate-950, Slate-900 (다크 모드)
- **Surface**: Slate-800/50 (반투명 글래스모피즘)
- **Border**: Slate-700/50

### 디자인 원칙
- **글래스모피즘**: backdrop-blur 효과를 활용한 반투명 UI
- **그라디언트**: 브랜드 컬러 기반의 부드러운 그라디언트
- **애니메이션**: 호버 시 scale, translate 효과
- **그리드 레이아웃**: 모든 리스트는 3컬럼 그리드

---

## 📐 레이아웃 구조

### 전체 구조
```
┌─────────────────────────────────────────┐
│  Sidebar (280px)  │   Main Content      │
│                   │                     │
│   Navigation      │   Active View       │
│   Menu            │   Content           │
│                   │                     │
│   System Status   │                     │
└─────────────────────────────────────────┘
```

### 사이드바 (Sidebar)
- **크기**: 280px 고정
- **구성요소**:
  1. 헤더 (로고 + 앱 이름)
  2. 네비게이션 메뉴 (5개 항목)
  3. 시스템 상태 표시

---

## 🧭 네비게이션 메뉴

### 1. Devices (장치 관리)
**아이콘**: Cpu  
**그라디언트**: Cyan → Blue

#### 기능 개요
로봇손 제품과 연결된 모든 장치를 실시간으로 모니터링하고 관리

#### UI 레이아웃
- 3컬럼 그리드 레이아웃
- 각 카드는 호버 시 약간 상승 효과

#### 장치 카드 구성 요소

**1. 헤더 섹션**
- 장치명 (예: "Robot Hand #1")
- 연결 상태 아이콘
  - 연결됨: Wifi 아이콘 (녹색)
  - 연결 끊김: WifiOff 아이콘 (빨간색)

**2. 상태 정보 패널**

| 상태 | 아이콘 | 표시 정보 |
|------|--------|-----------|
| 동작 상태 | Power | Operating / Idle |
| 오류 상태 | AlertTriangle / AlertCircle | Error Detected / No Errors |
| 배터리 | Battery / BatteryWarning | 배터리 퍼센트 + 프로그레스 바 |

**3. 액션 버튼**
- **Control 버튼**: 장치 조작 화면으로 이동
  - 스타일: 그라디언트 배경 (Primary 컬러)
  - 기능: 해당 장치의 실시간 제어 인터페이스 진입
- **Settings 버튼**: 장치 설정 화면으로 이동
  - 스타일: 세컨더리 버튼
  - 기능: 장치별 설정 (캘리브레이션, 펌웨어 업데이트 등)

#### 상태 인디케이터 상세

**연결 상태**
- ✅ Connected: 녹색 배지
- ❌ Disconnected: 빨간색 배지
- 실시간 WebSocket/MQTT 연결 모니터링

**오류 감지**
- 오류 있음: 빨간색 경고 아이콘
- 정상: 녹색 체크 아이콘
- 오류 발생 시 Logging 메뉴로 연결

**동작 상태**
- Operating: 현재 작업 수행 중
- Idle: 대기 상태
- 실시간 센서 데이터 기반 업데이트

**배터리 상태**
- 20% 이상: 녹색 프로그레스 바
- 20% 미만: 오렌지색 경고
- 프로그레스 바 시각화

---

### 2. Learning (학습 센터)
**아이콘**: BookOpen  
**그라디언트**: Purple → Pink

#### 기능 개요
사용자 교육을 위한 매뉴얼 문서 및 비디오 튜토리얼 제공

#### UI 구조
두 개의 독립적인 섹션으로 구성:

**섹션 1: Manuals (문서 매뉴얼)**

카드 구성:
- 그라디언트 아이콘 배지 (각 문서마다 고유 컬러)
- 문서 제목
- 페이지 수 표시
- 호버 시 스케일 업 애니메이션

문서 카테고리:
1. **Quick Start Guide** (빠른 시작 가이드)
   - 초보자용 기본 설정 가이드
   - 페이지: 12p
2. **Advanced Operations** (고급 작동법)
   - 전문 사용자를 위한 고급 기능
   - 페이지: 45p
3. **Troubleshooting** (문제 해결)
   - 일반적인 오류 해결 방법
   - 페이지: 28p
4. **Maintenance Guide** (유지보수 가이드)
   - 정기 점검 및 관리 매뉴얼
   - 페이지: 34p
5. **Safety Manual** (안전 매뉴얼)
   - 안전 수칙 및 주의사항
   - 페이지: 18p
6. **API Documentation** (API 문서)
   - 개발자용 API 레퍼런스
   - 페이지: 67p

**섹션 2: Video Tutorials (동영상 강의)**

카드 구성:
- 썸네일 영역 (그라디언트 배경)
- 재생 아이콘 (중앙 배치)
- 비디오 제목
- 재생 시간 및 조회수

비디오 콘텐츠:
1. **Basic Setup Tutorial** (기본 설정 튜토리얼)
   - 시간: 12:34
   - 조회수: 2.3K
2. **Advanced Programming** (고급 프로그래밍)
   - 시간: 28:15
   - 조회수: 1.8K
3. **Calibration Process** (캘리브레이션 과정)
   - 시간: 15:42
   - 조회수: 3.1K
4. **Error Recovery** (오류 복구)
   - 시간: 18:20
   - 조회수: 1.2K
5. **Maintenance Tips** (유지보수 팁)
   - 시간: 22:10
   - 조회수: 2.7K
6. **Best Practices** (모범 사례)
   - 시간: 31:45
   - 조회수: 4.2K

#### 인터랙션
- 매뉴얼 클릭: PDF 뷰어 또는 외부 브라우저로 오픈
- 비디오 클릭: 내장 비디오 플레이어 실행
- 검색 기능 (추후 구현 가능)
- 북마크/즐겨찾기 기능

---

### 3. Simulator (시뮬레이터)
**아이콘**: Monitor  
**그라디언트**: Green → Teal

#### 기능 개요
3D 뷰어를 통해 로봇의 동작을 시뮬레이션하고 실제 장치에 원격 명령 전송

#### 레이아웃
```
┌─────────────────────────────┬──────────────┐
│                             │              │
│   3D Viewer                 │   Motion     │
│   (2/3 width)               │   Script     │
│                             │   Panel      │
│   - Robot Selection         │   (1/3)      │
│   - 3D Mesh Display         │              │
│   - Control Panel           │              │
│                             │              │
└─────────────────────────────┴──────────────┘
```

#### 왼쪽 패널: 3D Viewer

**1. 로봇 선택 드롭다운**
- Devices에 등록된 모든 로봇 목록
- 선택 시 3D 모델 자동 로드
- 연결 상태에 따른 실시간 제어 가능 여부 표시

**2. 3D 렌더링 영역**
- Three.js 기반 3D 뷰어
- 기능:
  - 마우스 드래그로 회전
  - 스크롤로 줌 인/아웃
  - 그리드 배경 (깊이감 표현)
  - 조명 효과
- 로봇 메시 표시
  - 관절별 색상 구분
  - 실시간 포즈 업데이트

**3. 제어 버튼**
- **Execute Script**: 작성된 스크립트 실행
  - 시뮬레이터에서 먼저 동작 확인
  - 확인 후 실제 장치로 전송 옵션
- **Reset**: 로봇을 초기 포즈로 리셋

#### 오른쪽 패널: Motion Script

**스크립트 에디터 특징**
- 스크래치 스타일의 블록 기반 UI
- 각 스텝은 순차적으로 실행

**스크립트 스텝 구성**
```javascript
{
  id: unique_id,
  type: "pose" | "matrix" | "delay",
  data: {
    // 6D Pose 형식
    position: { x, y, z },
    rotation: { roll, pitch, yaw }
    // 또는 변환 행렬
    matrix: [4x4 matrix]
  }
}
```

**스텝 타입**

1. **6D Pose Input**
   - Position (x, y, z)
   - Rotation (roll, pitch, yaw)
   - 예: `Position(x:0, y:100, z:50)`

2. **Transformation Matrix**
   - 4×4 변환 행렬 입력
   - 고급 사용자용

3. **Delay**
   - 스텝 간 대기 시간
   - 밀리초 단위

**스크립트 관리 기능**
- ➕ Add Step: 새 스텝 추가
- 🗑️ Delete Step: 스텝 삭제
- ↕️ Reorder: 드래그앤드롭으로 순서 변경 (추후 구현)
- 💾 Save Script: 스크립트 저장 (추후 구현)
- 📂 Load Script: 저장된 스크립트 불러오기 (추후 구현)

#### 실행 프로세스

1. **시뮬레이션 모드**
   ```
   스크립트 작성 → Play 클릭 → 3D 뷰어에서 미리보기
   ```

2. **실제 장치 제어**
   ```
   시뮬레이션 확인 → "Send to Device" 버튼 클릭 → 
   실제 로봇으로 명령 전송 → 실행 상태 모니터링
   ```

#### 안전 기능
- 충돌 감지 (가상 환경)
- 관절 한계 검증
- 비정상 동작 경고
- 긴급 정지 버튼

---

### 4. Logging (로그 관리)
**아이콘**: Activity  
**그라디언트**: Orange → Red

#### 기능 개요
시스템 전체의 이벤트, 오류, 경고 메시지를 시간순으로 기록 및 표시

#### UI 구조
테이블 형식의 로그 뷰어

**테이블 컬럼**

| 컬럼명 | 설명 | 표시 형식 |
|--------|------|-----------|
| Time | 발생 시각 | HH:MM:SS (모노스페이스 폰트) |
| Type | 로그 레벨 | 컬러 배지 |
| Device | 발생 장치 | 장치명 |
| Message | 로그 내용 | 텍스트 |

#### 로그 타입 (Log Level)

**1. ERROR (오류)**
- 색상: 빨간색 (#EF4444)
- 예시:
  - Connection lost
  - Motor overheating
  - Sensor failure
  - Communication timeout

**2. WARNING (경고)**
- 색상: 오렌지색 (#F59E0B)
- 예시:
  - Low battery warning
  - High temperature
  - Calibration needed
  - Maintenance due

**3. INFO (정보)**
- 색상: 파란색 (#3B82F6)
- 예시:
  - Calibration completed
  - Firmware updated
  - Device connected
  - Script executed successfully

#### 기능

**필터링**
- 로그 타입별 필터 (Error, Warning, Info)
- 장치별 필터
- 시간 범위 필터
- 검색 기능 (키워드)

**정렬**
- 시간순 (최신순/오래된순)
- 로그 타입별
- 장치별

**내보내기**
- CSV 파일로 내보내기
- 텍스트 파일로 저장
- 선택한 로그만 내보내기

**실시간 업데이트**
- 새 로그 자동 추가
- 웹소켓 기반 실시간 스트리밍
- 알림 배지 (새 오류 발생 시)

**상세 보기**
- 로그 클릭 시 상세 정보 모달
- 스택 트레이스 (오류의 경우)
- 관련 로그 하이라이트

#### 로그 보관 정책
- 로컬 저장: 최근 30일
- 자동 정리: 30일 이상 된 로그 자동 삭제
- 수동 백업 기능 제공

---

### 5. Settings (설정)
**아이콘**: Settings  
**그라디언트**: Gray → Gray

#### 기능 개요
애플리케이션 전반의 설정 관리

#### 설정 카테고리

**1. 테마 설정**

카드 레이아웃:
- 제목: "Theme"
- 옵션:
  - 🌙 Dark Mode
  - ☀️ Light Mode
- 선택된 옵션: 그라디언트 배경 강조
- 실시간 적용

**2. 언어 설정**

지원 언어:
- 🇺🇸 English
- 🇰🇷 한국어
- 🇯🇵 日本語
- 🇨🇳 中文

드롭다운 선택:
- 선택 시 즉시 적용
- UI 텍스트 전체 번역
- i18n 라이브러리 활용

**3. 앱 정보**

표시 정보:
- **Version**: 1.0.0
- **Build**: 2025.10.12
- **License**: MIT / Proprietary
- **Developer**: [Company Name]
- **Website**: [URL]

추가 액션:
- Check for Updates (업데이트 확인)
- Release Notes (릴리즈 노트)
- About Dialog (정보 대화상자)

#### 추가 설정 항목 (향후 확장)

**알림 설정**
- 데스크탑 알림 활성화/비활성화
- 오류 발생 시 알림
- 배터리 부족 알림
- 작업 완료 알림

**네트워크 설정**
- 연결 프로토콜 (WebSocket/MQTT)
- 서버 주소
- 포트 번호
- 재연결 시도 횟수

**고급 설정**
- 로그 레벨
- 디버그 모드
- 개발자 도구
- 캐시 관리

**데이터 관리**
- 데이터 백업
- 데이터 복원
- 초기화

---

## 🔧 기술 사양

### Electron 메인 프로세스

**역할**
- 윈도우 관리
- 네이티브 API 접근
- IPC 통신

**주요 기능**
```javascript
- createWindow(): 메인 윈도우 생성
- handleDeviceConnection(): 장치 연결 관리
- handleFileOperations(): 파일 저장/불러오기
- handleUpdate(): 앱 업데이트
```

### Electron 렌더러 프로세스

**React 컴포넌트 구조**
```
App
├── Sidebar
│   ├── Logo
│   ├── Navigation
│   └── SystemStatus
└── MainContent
    ├── DevicesView
    ├── LearningView
    ├── SimulatorView
    │   ├── ThreeJsViewer
    │   └── ScriptEditor
    ├── LoggingView
    └── SettingsView
```

### 상태 관리

**React State**
- 로컬 컴포넌트 상태: useState
- 복잡한 상태: useReducer
- 전역 상태: Context API 또는 Redux

**상태 항목**
```javascript
{
  devices: [...],          // 연결된 장치 목록
  selectedDevice: null,    // 현재 선택된 장치
  scriptSteps: [...],      // 시뮬레이터 스크립트
  logs: [...],             // 로그 데이터
  theme: 'dark',           // 테마
  language: 'ko'           // 언어
}
```

### 통신 프로토콜

**장치 통신**
- WebSocket 또는 MQTT
- 실시간 양방향 통신
- JSON 기반 메시지 포맷

**메시지 포맷 예시**
```json
{
  "type": "command",
  "device_id": "robot_hand_1",
  "action": "move",
  "data": {
    "position": [0, 0, 0],
    "rotation": [0, 0, 0]
  },
  "timestamp": 1234567890
}
```

---

## 📊 데이터 모델

### Device (장치)
```typescript
interface Device {
  id: string;
  name: string;
  type: 'robot_hand';
  connected: boolean;
  error: boolean;
  operating: boolean;
  battery: number;
  lastUpdate: Date;
  firmwareVersion: string;
  serialNumber: string;
}
```

### ScriptStep (스크립트 단계)
```typescript
interface ScriptStep {
  id: string;
  order: number;
  type: 'pose' | 'matrix' | 'delay';
  data: {
    position?: { x: number; y: number; z: number };
    rotation?: { roll: number; pitch: number; yaw: number };
    matrix?: number[][];
    duration?: number;
  };
}
```

### Log (로그)
```typescript
interface Log {
  id: string;
  timestamp: Date;
  type: 'error' | 'warning' | 'info';
  device_id: string;
  message: string;
  details?: any;
}
```

---

## 🚀 개발 로드맵

### Phase 1: MVP (최소 기능 제품)
- ✅ UI/UX 디자인 완성
- ✅ 기본 네비게이션
- ✅ Devices 뷰 (읽기 전용)
- ✅ Learning 뷰 (정적 콘텐츠)
- ✅ Settings 뷰 (테마/언어)

### Phase 2: 핵심 기능
- ⬜ 실제 장치 연결 (WebSocket)
- ⬜ 실시간 상태 모니터링
- ⬜ Simulator 3D 뷰어 (Three.js)
- ⬜ 기본 스크립트 실행
- ⬜ Logging 시스템

### Phase 3: 고급 기능
- ⬜ 스크립트 저장/불러오기
- ⬜ 복잡한 동작 시퀀스
- ⬜ 충돌 감지
- ⬜ 비디오 스트리밍
- ⬜ 원격 펌웨어 업데이트

### Phase 4: 최적화 및 확장
- ⬜ 성능 최적화
- ⬜ 다국어 완성
- ⬜ 오프라인 모드
- ⬜ 클라우드 동기화
- ⬜ 플러그인 시스템

---

## 🔒 보안 고려사항

### 통신 보안
- TLS/SSL 암호화
- 장치 인증
- 토큰 기반 세션 관리

### 데이터 보안
- 로컬 데이터 암호화
- 민감 정보 보호
- 안전한 업데이트 프로세스

### 안전 기능
- 긴급 정지 버튼
- 동작 범위 제한
- 오작동 감지 및 자동 정지

---

## 📈 성능 목표

- 앱 시작 시간: < 2초
- UI 반응 시간: < 100ms
- 3D 렌더링: 60 FPS
- 통신 지연: < 50ms
- 메모리 사용: < 500MB

---

## 🧪 테스트 계획

### 단위 테스트
- React 컴포넌트 테스트
- 유틸리티 함수 테스트
- 상태 관리 테스트

### 통합 테스트
- IPC 통신 테스트
- 장치 연결 테스트
- 데이터 흐름 테스트

### E2E 테스트
- 사용자 시나리오 테스트
- 크로스 플랫폼 테스트
- 성능 테스트

---

## 📱 배포

### 플랫폼
- Windows (x64, ARM64)
- macOS (Intel, Apple Silicon)
- Linux (x64)

### 배포 패키지
- 설치 프로그램 (.exe, .dmg, .deb)
- 포터블 버전 (zip)
- 자동 업데이트 지원

---

## 📞 지원 및 피드백

### 사용자 지원
- 인앱 헬프 시스템
- 이메일 지원
- 커뮤니티 포럼

### 피드백 수집
- 버그 리포트
- 기능 요청
- 사용성 개선

---

## 📄 라이선스
[라이선스 정보를 여기에 추가]

---

**문서 버전**: 1.0  
**최종 수정일**: 2025-10-18  
**작성자**: [작성자명]
