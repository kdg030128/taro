# 타로카드 디자인 시스템 — DESIGN.md
> 르네상스 갤러리 위의 양피지 타로 (Renaissance Gallery on Putty Paper)

**Theme:** Renaissance Gallery / Minimalist Editorial / Monochrome Warmth  
**Target Platform:** Mobile Web First (iOS / Android), Responsive

---

## 1. 디자인 철학 및 비주얼 콘셉트

본 디자인 시스템은 타로카드를 흔한 키치(kitsch)나 보라색 네온풍의 마법 콘셉트가 아닌, **'고전 미술관(Gallery)에 전시된 르네상스 판화와 양피지 문서'**라는 엄숙하고 세련된 시각 언어로 재해석합니다.

* **양피지 캔버스(Putty Paper)**: 차가운 순백색 대신 따뜻한 회갈색(Putty `#c4c3b6`)과 뼈색(Bone `#e7e5e4`)을 바탕으로 사용하여 고문서나 미술관 전시 벽면의 질감을 전달합니다.
* **흑백 콘트라스트와 극도로 절제된 컬러**: 화려한 원색을 배제하고 깊은 먹색(Ink `#000000`)과 절제된 그레이 스케일만으로 신비감과 신뢰도를 형성합니다.
* **기능적 모던 그로테스크 × 고전 세리프의 대비**:
  - 카드 이름, 메인 타이틀, 운명적 키워드는 고전적인 **Serif**로 우아함을 극대화합니다.
  - 모바일 가독성이 중요한 입력 폼, 안내문, 3줄 맞춤 해석문은 높은 가독성의 **Grotesk(Sans-serif)**가 담당합니다.
* **플랫과 헤어라인(Hairline)**: 입체 효과나 인위적인 그림자(Drop Shadow), 그라데이션을 완전히 배제하고, 인쇄물의 재단선 같은 극세선(Hairline Border `#dfdcd5`)과 면의 교차로 계층을 만듭니다.

---

## 2. 디자인 토큰 — Color Palette

### 2.1 기본 팔레트 (Primitives)

| 토큰명 | HEX | 역할 및 가이드 |
|---|---|---|
| `--color-putty` | `#c4c3b6` | **기본 배경 캔버스 (Level 0)**. 화면 전반에 흐르는 따뜻한 회갈색 바탕 |
| `--color-bone` | `#e7e5e4` | **카드 및 엘리베이션 표면 (Level 1)**. 결과 카드 및 입력 컨테이너 |
| `--color-chalk` | `#ebebeb` | **가장 밝은 보조 표면 (Level 2)**. 알림 박스 및 보조 배경 |
| `--color-ink` | `#000000` | **주요 텍스트 & Primary 버튼**. 모든 중요한 액션 및 타이틀 |
| `--color-vellum` | `#dfdcd5` | **헤어라인 보더 (Hairline Border)**. 양피지 종이 가장자리 느낌의 1px 경계선 |
| `--color-graphite` | `#595855` | **보조/플레이스홀더 텍스트**. 과한 대비를 줄여주는 차분한 웜 그레이 |
| `--color-ash` | `#808080` | **카드 이미지 플레이스홀더 및 비활성 상태**. 중립 회색 |
| `--color-paper` | `#ffffff` | **다크 서피스 반전 텍스트 & 순백색 액센트**. 카드 배경 내부 캔버스 |

### 2.2 shadcn / Tailwind 시맨틱 토큰 매핑 (CSS Variables)

Tailwind CSS v4 및 shadcn/ui 표준 시맨틱 변수 체계에 맞춘 매핑입니다:

```css
:root {
  /* Canvas & Base */
  --background: #c4c3b6;          /* Putty */
  --foreground: #000000;          /* Ink */

  /* Surfaces & Containers */
  --card: #e7e5e4;                /* Bone */
  --card-foreground: #000000;     /* Ink */
  --popover: #e7e5e4;             /* Bone */
  --popover-foreground: #000000;  /* Ink */

  /* Primary Interactive (Pill Button, Active Chips) */
  --primary: #000000;             /* Ink */
  --primary-foreground: #ffffff;  /* Paper */

  /* Secondary Interactive (Outline, Topic Chips) */
  --secondary: #dfdcd5;           /* Vellum */
  --secondary-foreground: #000000;/* Ink */

  /* Muted & Neutral States */
  --muted: #dfdcd5;               /* Vellum */
  --muted-foreground: #595855;    /* Graphite */

  /* Borders & Inputs */
  --border: #dfdcd5;              /* Vellum */
  --input: #dfdcd5;               /* Vellum */
  --ring: #000000;                /* Ink */

  /* Radius System */
  --radius: 9px;                  /* 기본 카드 라운딩 */
  --radius-pill: 28.8px;          /* 액션 버튼 및 칩 */
}
```

---

## 3. 타이포그래피 (Typography)

### 3.1 폰트 패밀리 구성

1. **Display & Serif (`--font-serif`)**:
   - 추천: `Cormorant Garamond`, `Playfair Display`, `Cinzel`, `Canela`
   - 영문 카드 번호(XIX), 카드 명칭(THE SUN), 헤더 타이틀, 별자리 기호에 적용
2. **Body & Utility Grotesk (`--font-sans`)**:
   - 추천: `Pretendard`, `Helvetica Now`, `Inter`, `Noto Sans KR`
   - 한글 맞춤 해석(3줄), 입력 폼 필드, 버튼 라벨, 안내 문구에 적용

### 3.2 타입 스케일 (Type Scale)

| 역할 | 적용 대상 | 크기 / 행간 | 자간 | 굵기 |
|---|---|---|---|---|
| **Display** | 카드 로마숫자 · 메인 심볼 | 36px / 1.0 | -0.04em | 500 (Medium) |
| **Title 1** | 카드 정식 명칭 (XIX 태양) | 24px / 1.2 | -0.02em | 500 (Medium Serif) |
| **Title 2** | 화면 헤더 타이틀 · 섹션명 | 20px / 1.3 | -0.01em | 500 (Medium) |
| **Body Large** | 맞춤 해석 3줄 본문 (F-4) | 16px / 1.6 | -0.01em | 400 (Regular Sans) |
| **Body** | 폼 입력 텍스트 · 주요 안내 | 15px / 1.5 | normal | 400 (Regular) |
| **Label** | 버튼 텍스트 · 칩 라벨 | 13px / 1.2 | +0.02em | 500 (Medium) |
| **Caption** | 오락용 안내 · 개인정보 폐기 안내 | 12px / 1.4 | normal | 400 (Muted Graphite) |
| **Micro** | 카드 하단 저작권 · 서비스 워터마크 | 10px / 1.2 | +0.05em | 500 (Uppercase) |

---

## 4. 컴포넌트 규격 (Components & shadcn/ui)

### 4.1 필 버튼 (Pill Action Button)
* **역할**: 주요 전환 액션 ([타로 시작], [카드 한 장 뽑기], [이미지 저장], [결과 공유])
* **스타일**:
  - `bg-[#000000] text-[#ffffff] font-medium text-[14px]`
  - 패딩: `px-6 py-3.5` (모바일 터치 타깃 48px 이상 보장)
  - 보더 반경: `rounded-full` (28.8px)
  - 상태:
    - **Hover/Active**: `hover:bg-[#1f1e1d] active:scale-[0.98] transition-transform`
    - **Disabled**: `bg-[#dfdcd5] text-[#808080] cursor-not-allowed`

### 4.2 주제 선택 칩 (Topic Selection Chips)
* **역할**: 6대 주제 선택 (커리어, 재물, 연애, 건강, 학업, 종합)
* **스타일**:
  - 미선택: `bg-[#e7e5e4] border border-[#dfdcd5] text-[#000000] rounded-full px-4 py-2 text-sm`
  - 선택됨: `bg-[#000000] text-[#ffffff] border-black rounded-full px-4 py-2 text-sm font-medium`
  - 트랜지션: `transition-all duration-150`

### 4.3 폼 인풋 필드 (Form Input)
* **역할**: 이름(최대 10자), 생년월일(YYYY.MM.DD), 전공(선택)
* **스타일**:
  - 배경: `bg-[#e7e5e4]` (Bone Card Surface)
  - 보더: `border border-[#dfdcd5] focus:border-[#000000] focus:ring-1 focus:ring-[#000000]`
  - 보더 반경: `rounded-[9px]`
  - 플레이스홀더: `text-[#595855]` (Graphite)
  - 에러 상태: 붉은색 대신 `border-[#000000] text-[#000000]`와 안내 캡션("날짜를 다시 확인해 주세요") 표시

### 4.4 타로 카드 뒤집기 애니메이션 (Tarot Card Container)
* **역할**: F-3 카드 뽑기 시 1초 이내 정방향 플립
* **스펙**:
  - 비율: `aspect-[1/1.65]` (폭 220px ~ 260px 모바일 적정 사이즈)
  - 3D 트랜스폼:
    ```css
    .perspective-card { perspective: 1000px; }
    .card-inner {
      transform-style: preserve-3d;
      transition: transform 0.8s cubic-bezier(0.2, 0.8, 0.2, 1);
    }
    .card-flipped { transform: rotateY(180deg); }
    .card-front, .card-back {
      backface-visibility: hidden;
      border-radius: 9px;
      border: 1px solid #dfdcd5;
    }
    .card-front { transform: rotateY(180deg); }
    ```
  - 뒷면 그래픽: 르네상스 기하학 문양 또는 앤틱 스타 패턴
  - 앞면 그래픽: 22장 메이저 아르카나 고전 판화풍 일러스트

### 4.5 결과 저장 카드 (S-03 & 1080×1350 이미지 규격)
* **역할**: [이미지 저장] 시 PNG 파일로 렌더링되는 기준 캔버스
* **규격**:
  - 캔버스 비율: **4:5 (1080px × 1350px)**
  - 배경색: `#e7e5e4` (Bone)
  - 외곽선: `1px solid #dfdcd5` (Vellum)
  - 내부 패딩: `48px` (실제 다운로드 이미지 기준)
  - 구성 요소 배치:
    1. 상단: `{이름}님의 타로 · {주제}` (13px Grotesk Muted)
    2. 중앙 상단: 카드 일러스트레이션 (프레임 테두리 포함)
    3. 중앙: `{로마숫자} {카드이름} · {별자리기호} {별자리이름}` (20px Serif)
    4. 중앙 하단: **맞춤 해석 3줄** (15px Grotesk, 1.6 Line-height, 최대 90자 이내)
    5. 하단: `※ 오락용 타로 해석입니다` (11px Graphite)
    6. 푸터: 서비스 브랜딩 워터마크

### 4.6 안내 및 정보 폐기 콜아웃 (Privacy Notice Box)
* **역할**: "개인정보는 서버로 전송/저장하지 않고 창을 닫으면 지워집니다" 안내
* **스타일**:
  - `bg-[#ebebeb] border border-[#dfdcd5] text-[#595855] text-[12px] p-3 rounded-[9px]`
  - 잠금 아이콘(`🔒`) 또는 미니멀 갤러리 심볼 포함

### 4.7 알림 토스트 (Toast Feedback)
* **역할**: "이미지를 저장했어요", "결과를 복사했어요" 피드백
* **스타일**:
  - `bg-[#000000] text-[#ffffff] px-4 py-2.5 rounded-full text-xs font-medium`
  - 중앙 하단 플로팅, 2초 후 부드럽게 페이드아웃

---

## 5. 모바일 화면별 레이아웃 가이드

```
S-01 시작 화면                  S-02 정보 입력 화면              S-03 결과 화면
┌─────────────────────────┐   ┌─────────────────────────┐   ┌─────────────────────────┐
│        [ 🏛️ ]           │   │ ← 뒤로가기              │   │ [결과 카드 컨테이너]    │
│                         │   │                         │   │ ┌─────────────────────┐ │
│       오늘의 타로       │   │ 이름 (닉네임)           │   │ │ 지민님의 타로 · 커리어│ │
│   [ 르네상스 카드 뒷면 ] │   │ [ ____________ ]        │   │ │   [ 태양 카드 ]     │ │
│                         │   │ 생년월일 (YYYY.MM.DD)   │   │ │ XIX THE SUN · ♌    │ │
│  생년월일과 전공으로    │   │ [ ____________ ]        │   │ │                       │ │
│  나만의 해석을 만나요   │   │ 전공 (선택)             │   │ │ 3줄 맞춤 해석문       │ │
│                         │   │ [ ____________ ]        │   │ │ (기본+별자리+전공)    │ │
│  [     타로 시작     ]  │   │                         │   │ └─────────────────────┘ │
│                         │   │ 주제 선택 (6개 칩)      │   │ [ 이미지 저장 ] [ 공유 ]│
│ ※ 오락용 · 저장 안 함   │   │ [커리어] [재물] [연애]  │   │ [ 다시 뽑기 ] [ 처음으로]│
│                         │   │ 🔒 개인정보 안내문      │   │ 🔒 정보 즉시 폐기 안내  │
│                         │   │ [ 카드 한 장 뽑기 (Pill)│   │                         │
└─────────────────────────┘   └─────────────────────────┘   └─────────────────────────┘
```

---

## 6. Do & Don't 가이드

### Do (권장)
- **자연스러운 갤러리 분위기 유지**: 배경은 항상 `#c4c3b6` (Putty)를 기본으로 하고, 컨테이너는 `#e7e5e4` (Bone)으로 1단계만 부드럽게 올립니다.
- **헤어라인 보더 활용**: 구분이 필요한 모든 곳에는 두꺼운 선이나 그림자 대신 `1px solid #dfdcd5`를 적용합니다.
- **철저한 타이포 계층 분리**: 제목과 카드명은 Serif, 3줄 해석과 본문/입력란은 Sans-serif로 명확히 나눕니다.
- **풀 필 버튼 사용**: 주요 액션은 `rounded-full` 캡슐 형태를 유지하여 손가락 탭 경험을 최적화합니다.

### Don't (금지)
- **원색(Primary Colors) 사용 금지**: 빨강, 파랑, 보라색 네온 컬러를 일체 사용하지 않습니다.
- **인위적인 드롭 섀도우(Drop Shadow) 금지**: 모든 요소는 평면(Flat)으로 유지하며, 그림자로 입체감을 만들지 않습니다.
- **그라데이션(Gradient) 금지**: 캔버스와 버튼에 인위적인 색상 변화 그라데이션을 넣지 않습니다.
- **해석 본문에 Serif 사용 금지**: 3줄 맞춤 해석은 모바일 화면에서 빠르게 읽혀야 하므로 가독성이 높은 Sans-serif를 유지합니다.

---

## 7. 구현 코드 스니펫

### 7.1 Tailwind CSS v4 `@theme` 설정 (`globals.css`)

```css
@import "tailwindcss";

@theme {
  /* Colors */
  --color-putty: #c4c3b6;
  --color-ink: #000000;
  --color-bone: #e7e5e4;
  --color-chalk: #ebebeb;
  --color-vellum: #dfdcd5;
  --color-graphite: #595855;
  --color-ash: #808080;
  --color-paper: #ffffff;

  /* Font Families */
  --font-serif: 'Cormorant Garamond', 'Playfair Display', serif;
  --font-sans: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;

  /* Border Radius */
  --radius-card: 9px;
  --radius-pill: 28.8px;
}
```

### 7.2 주요 컴포넌트 Tailwind 클래스 조합

* **페이지 래퍼**: `min-h-screen bg-[#c4c3b6] text-[#000000] font-sans flex flex-col items-center px-4 py-8`
* **중앙 모바일 컨테이너**: `w-full max-w-[420px] flex flex-col gap-6`
* **카드 프레임**: `bg-[#e7e5e4] border border-[#dfdcd5] rounded-[9px] p-6 flex flex-col items-center`
* **주요 액션 버튼**: `w-full h-12 bg-[#000000] text-[#ffffff] rounded-full font-medium text-sm transition-transform active:scale-[0.98] disabled:bg-[#dfdcd5] disabled:text-[#808080]`
* **보조 버튼 (아웃라인)**: `w-full h-12 bg-transparent border border-[#000000] text-[#000000] rounded-full font-medium text-sm transition-colors hover:bg-[#000000] hover:text-[#ffffff]`
* **개인정보 안내문구 박스**: `bg-[#ebebeb] border border-[#dfdcd5] rounded-[9px] p-3 text-xs text-[#595855] leading-relaxed`
