# GLUCK 실시간 견적 페이지 프로토타입 V43

산업용 SLA 3D프린팅 양산 제조 기업 **GLUCK**의 실시간 견적 페이지 프로토타입입니다. STL 파일을 업로드하면 브라우저에서 즉시 메시 분석·DfM 검토·예상 견적을 산출합니다.

**🔗 Live Demo:** https://gluck3dprinting.github.io/gluck-quote-prototype/

---

## 주요 기능

### 📤 파일 업로드 + 즉시 분석
- 드래그 앤 드롭 / 다중 파일 업로드 지원
- 지원 형식: `.stl`, `.obj`, `.step`, `.stp`, `.3mf`, `.zip`
- 업로드 즉시 부피·치수·면적·삼각형 수 분석
- 분석 신뢰도 표시 (`frontend-geometry` / `frontend-mock`)

### 🔬 실제 STL 지오메트리 분석
- **Gauss divergence theorem** 기반 정확한 부피 계산
- **Edge topology** 기반 hole 검출 (Open mesh boundary edge)
- Non-manifold 메시 감지
- 빌드 사이즈(350×350×300mm) 초과 시 분할 안내
- 자동 면 방향 보정

### 🎨 3D 뷰어
- Three.js 기반 인터랙티브 회전·줌·팬
- 일반 / 투명 뷰 모드
- 스케일 비교 큐브 (100 / 300 / 500mm 선택)
- DfM 오류 시각화:
  - 🔴 Open mesh / Hole (빨간 영역)
  - 🔵 Thin wall (파란 영역, ≤1.0mm)
  - 🟠 Non-manifold edges

### ⚙️ 모델 조정
- 스케일 조정 (50~300%)
- 축별 회전 (X / Y / Z, 0° / 90° / 180° / 270°)
- 실시간 시각 반영 + 바닥 정렬 자동 보정
- 변경 시 견적 자동 무효화

### 🪣 속 비우기 (Hollowing) 시뮬레이션
- GLUCK 표준 벽두께 **2T (2mm)** 기준
- Vertex normal offset 기반 내벽 부피 시뮬레이션
- 절감 비율 5% 이상 파트만 적용 가능 (자동 판정)
- Thin wall 검출 시 자동 제외
- 프로젝트 전체 일괄 적용 버튼

### 📋 제조성 검토 알림
- Hole / Thin wall / Non-manifold / 빌드 초과 통합 카드
- 자동 검출 + 시각화 + 텍스트 안내
- "정상" / "검토 필요" 상태 라벨

### 💰 견적 산출
- 재료별 단가 적용 (G10-BR / G40-JG / G40-GW)
- 속 비우기 절감 반영
- 파트별 + 프로젝트 합계
- 양산 단가 별도 안내 (정식 견적 요청 유도)

### 🔄 다중 파트 관리
- 좌측 사이드바에서 파트 목록 관리
- 복제 / 삭제 / 전체 삭제
- 파트별 독립 옵션 (재료 / 수량 / 회전 / 스케일)

---

## 기술 스택

| 영역 | 사용 기술 |
|---|---|
| **프레임워크** | React 18 (CDN) |
| **3D 렌더링** | Three.js r128 |
| **STL 파싱** | Three.js STLLoader |
| **메시 분석** | 자체 구현 (Gauss volume, edge topology) |
| **스타일** | Tailwind CSS (CDN, JIT 컴파일) |
| **번들** | 단일 HTML 파일 (빌드 도구 없음) |
| **호스팅** | GitHub Pages |

> **참고:** 빌드 단계 없이 단일 HTML 파일로 동작합니다. CDN 의존성을 최소화하면서 즉시 배포 가능한 구조입니다.

---

## 디렉토리 구조

```
gluck-quote-prototype/
├── index.html        # 메인 페이지 (모든 코드 포함)
└── README.md         # 이 문서
```

단일 파일 구조라 별도 빌드/번들링 없이 `index.html`만으로 동작합니다.

---

## 로컬 개발

```bash
# 1. 레포 클론
git clone https://github.com/gluck3dprinting/gluck-quote-prototype.git
cd gluck-quote-prototype

# 2. 로컬 서버 실행 (Python)
python3 -m http.server 8000
# 또는 Node.js
npx serve .

# 3. 브라우저에서 접속
# http://localhost:8000
```

> CDN 라이브러리(React, Three.js, Tailwind)는 외부에서 자동 로드되므로 인터넷 연결 필요.

---

## GLUCK 제조 표준

프로토타입에 반영된 GLUCK 실무 기준:

| 항목 | 값 |
|---|---|
| **빌드 사이즈** | 350 × 350 × 300 mm |
| **속비우기 표준 벽두께** | 2T (2 mm) |
| **Thin wall 기준** | ≤ 1.0 mm |
| **재료 라인업** | G10-BR (범용·시제품) / G40-JG (고강도) / G40-GW (화이트) |
| **프린팅 방식** | SLA (광경화성 레진) |

---

## 라이센스 / 사용 안내

본 프로토타입은 GLUCK 내부 견적 시스템 설계·검증 목적의 데모입니다. 본 코드 또는 출력 결과를 다음 용도로 사용하지 않습니다:

- 실제 양산 견적 확정 (정식 견적 별도 진행)
- 글룩이 아닌 타사 견적 시스템에 그대로 이식
- 무단 복제·재배포

견적 결과는 자동 분석 기반 **예상 값**이며, 정식 견적은 GLUCK 엔지니어 검토 후 확정됩니다.

---

## 알려진 한계

- **메시 자동 복구 없음**: 프론트엔드 환경에서 `fix_normals` / `fill_holes` 미지원. 손상된 STL은 일부 분석 정확도 저하 가능
- **Vertex normal offset 한계**: 큐브형 부품의 속비우기 절감률 추정이 곡면 부품보다 낮게 산출됨
- **DfM 임계값**: 일반 STL 휴리스틱 기반. 글룩 실 부품으로 추가 검증 필요
- **백엔드 미연동**: 정밀 분석(trimesh)은 백엔드 API 구축 이후 적용 예정

---

## 문의

GLUCK Lab · https://glucklab.com
