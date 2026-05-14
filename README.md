# GLUCK 실시간 견적 페이지 (프로토타입 v24)

산업용 SLA 3D프린팅 양산 의사결정을 돕는 **실시간 견적 페이지 프로토타입**입니다.
글룩이 단순 출력 업체가 아닌 **디지털 파운드리**라는 본질을 페이지에 담는 것을 목표로 합니다.

> ⚠️ 내부 테스트용 프로토타입입니다. 실제 견적은 [glucklab.com](https://glucklab.com/estimate/real-time_estimate.html?lang=ko)에서 확인해주세요.

---

## 🔗 라이브 데모

**[https://gluck3dprinting.github.io/gluck-quote-prototype/](https://gluck3dprinting.github.io/gluck-quote-prototype/)**

---

## v24 핵심 기능 (Phase 6)

### 실제 geometry 분석
- STL/OBJ 파일을 업로드하면 **진짜 vertex 좌표 기반으로 분석**
- 치수 (BBox), 부피 (Gauss divergence theorem), 표면적, Open Mesh 검출, Non-manifold 검출
- 분석 신뢰도 점 표시: 🟢 실제 분석 / 🟡 분석 중

### 멀티 파트 프로젝트
- 여러 STL 파일을 한 프로젝트로 관리
- 파트별 재료·수량·속비우기 독립 설정

### 스케일 + 로테이트 (기본 접힘)
- 50~300% 스케일 조정
- X/Y/Z 축 0/90/180/270° 회전
- 회전 후에도 모델이 그리드 바닥에 정렬

### DfM 검사
- **Open Mesh / Hole** (빨강) — 진짜 boundary edge 기반
- **Thin Wall** (파랑, 1.0mm 기준) — 휴리스틱, 정밀 분석은 정식 견적에서
- **Non-manifold** (황색) — STL 정리 권장 안내

### 시각 도구
- 100mm 기준 큐브 토글 (모델 옆에 별도 표시, 견적 미포함)
- 일반 / 투명 모드 전환
- 자동 회전 + 마우스 드래그

### 영업 우선 흐름
- 옵션 패널: 프린팅 방식 → 재료 → 수량 → 견적 → (보조: 스케일·회전)
- 재료 hover 상세 설명 (잘림 없음, viewport 경계 자동 반전)
- 재료 cm³당 단가는 **외부 노출 금지**

---

## 테스트 방법

1. 라이브 데모 링크 접속
2. STL/OBJ 파일 드래그앤드롭 (Thingiverse, GrabCAD에서 무료 다운로드 가능)
3. 자동 분석 완료 후 옵션 선택 → **견적 계산하기**
4. 페이지 하단 **CRM 데이터 미리보기** 펼쳐서 JSON 구조 확인

---

## 기술 스택

- React 18 (CDN)
- Three.js r128 + STLLoader/OBJLoader
- Tailwind CSS (글룩 디자인시스템 토큰)
- SUIT Variable Font

단일 HTML 파일로 동작 (별도 빌드/서버 불필요).

---

## 버전 히스토리

| Version | Phase | 주요 변경 |
|---|---|---|
| **v24** | **Phase 6** | **실제 geometry 분석 (BBox·부피·표면적·DfM)** |
| v23 | Phase 5.1 | 재료 순서 변경 (G10-BR 우선), cm³당 단가 외부 노출 제거 |
| v22 | Phase 5 | 옵션 정보 위계 재배치 (스케일·회전 기본 접힘) |
| v21 | Phase 4 | 100mm 기준 큐브, 재료 hover Portal tooltip |
| v20 | Phase 3 | 회전 좌표계 통합 (partGroup) |
| v19 | Phase 2 | 스케일 + 로테이트 기본 |
| v18 | Phase 1 | 복잡도 삭제, 단가 정정, BBox 디자인, 색상 구분, CRM 구조 |
| v17 이전 | — | 멀티파트 구조, 3D 뷰어 기초 |

---

## 피드백 채널

- 사내 슬랙: `#gluck-product`
- 이슈 등록: [Issues](../../issues)
