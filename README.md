# 🧪 gray-scott-reaction-diffusion

> WebGL/GLSL 기반 그레이-스콧(피셔) 반응-확산 시뮬레이션 — 산호·뇌 주름·튜링 패턴이 실시간으로 자라나는 인터랙티브 데모

마우스 클릭으로 화학 물질을 투입하면 화면 가득 복잡하고 유기적인 무늬가 자라고, 6가지 프리셋(Coral / Mitosis / Spots / Worms / Holes / Spirals) 사이를 오가며 완전히 다른 형태의 자기 조직화 패턴을 관찰할 수 있습니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모 (Live Demo)

> **👉 [https://gray-scott-reaction-diffusion.vercel.app/](https://gray-scott-reaction-diffusion.vercel.app/)** — 브라우저에서 바로 실행 (GPU 가속)

| | |
|---|---|
| ![Demo](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fgray--scott--reaction--diffusion-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/gray-scott-reaction-diffusion) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-WebGL%2FGLSL-5586FF?style=flat-square&logo=webgl&logoColor=white) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **마우스 클릭 / 드래그** — 화학 물질 B 투입 → 패턴 교란·분기
3. **오른쪽 패널 슬라이더** — `f`(feed), `k`(kill), `B`(브러시 크기) 실시간 조정
4. **프리셋 버튼** — Coral · Mitosis · Spots · Worms · Holes · Spirals 전환
5. **단축키** — `space` = 일시정지 · `r` = 리셋 · `n` = 랜덤 시드

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/gray-scott-reaction-diffusion`](https://github.com/sigco3111/gray-scott-reaction-diffusion) |
| **라이브 데모** | [https://gray-scott-reaction-diffusion.vercel.app/](https://gray-scott-reaction-diffusion.vercel.app/) |
| **라이선스** | MIT |
| **의존성** | 없음 (Vanilla WebGL/GLSL, 단일 HTML) |

### 📝 사용된 프롬프트 (원문)

```
생물학적 패턴을 모방하는 그레이-스콧(Gray-Scott) 반응-확산 알고리즘을 GLSL 쉐이더로 구현하여,
화면 전체에 마치 산호초나 뇌의 주름처럼 복잡하고 유기적인 무늬가 실시간으로 성장하고 변화하는
과정을 시각화하되, 마우스로 클릭하는 지점에 화학 물질을 투입하여 패턴의 흐름을 방해하거나
새로운 무늬를 만들어내는 기능을 넣어줘.

Implementation Advice: WebGL (GLSL) is mandatory for speed here (Reaction-Diffusion is
computationally expensive). Use Ping-Pong buffering (swapping two textures) to simulate
the time steps of the chemical reaction. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로
코드 작성.
```

---

## ✨ 주요 특징 (Features)

- ⚡ **WebGL/GLSL 프래그먼트 셰이더** — 픽셀 단위 병렬 계산, 60fps 안정
- 🔄 **Ping-Pong 버퍼링** — 두 텍스처를 매 프레임 swap하며 시간 단계(dt) 시뮬레이션
- 🖱️ **마우스 인터랙션** — 클릭/드래그로 화학 B 농도 주입 → 패턴 교란
- 🎛️ **실시간 슬라이더** — `f`(feed), `k`(kill), 브러시 크기 즉시 조정
- 🎨 **6개 프리셋** — Coral / Mitosis / Spots / Worms / Holes / Spirals
- ⌨️ **키보드 단축키** — space(일시정지), r(리셋), n(랜덤)
- 📦 **단일 HTML** — 외부 의존성 0개, 파일 하나만 열면 실행
- 🔒 **온디바이스** — GPU 시뮬레이션이 브라우저 안에서만 처리됨

---

## 🚀 실행 방법 (Quick Start)

### 방법 1: 라이브 데모 (가장 간단)
👉 [https://gray-scott-reaction-diffusion.vercel.app/](https://gray-scott-reaction-diffusion.vercel.app/) — 클릭 한 번

### 방법 2: 그냥 브라우저로 열기
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 3: 로컬 서버 (권장 — 일부 브라우저는 file:// CORS 제한)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

---

## 🎮 조작법 (Controls)

| 입력 | 효과 |
|---|---|
| **마우스 클릭** | 클릭 지점에 화학 B 투입 → 패턴 교란 |
| **마우스 드래그** | 연속 주입 → 패턴 흐름 방해 / 새 가지 생성 |
| **슬라이더 `f`** | feed rate (0.010~0.100) — 화학 A 보충 속도 |
| **슬라이더 `k`** | kill rate (0.030~0.075) — 화학 B 제거 속도 |
| **슬라이더 `B`** | 브러시 크기 (2~48 px) — 주입 범위 |
| **`space`** | 일시정지 / 재개 |
| **`r`** | 현재 시드로 리셋 |
| **`n`** | 새 랜덤 시드 |

### Gray-Scott 프리셋 (f, k)

| 프리셋 | f | k | 패턴 |
|---|---|---|---|
| **Coral** | 0.062 | 0.062 | 산호 가지 (기본값) |
| **Mitosis** | 0.0367 | 0.0649 | 분열하는 세포 |
| **Spots** | 0.035 | 0.065 | 안정된 점 |
| **Worms** | 0.078 | 0.061 | 기어가는 벌레 |
| **Holes** | 0.039 | 0.058 | 스위스 치즈 |
| **Spirals** | 0.018 | 0.051 | 천천히 도는 나선 |

---

## 🛠️ 기술 스택 (Tech Stack)

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | WebGL 2.0 / GLSL ES 3.0 Fragment Shader |
| **시뮬레이션** | Ping-Pong Framebuffer (FBO swap) |
| **수치해석** | 5-point Laplacian stencil + semi-implicit Euler |
| **입력** | Canvas pointer events (mouse + touch) |
| **UI** | 순수 HTML + CSS + Vanilla JS (no framework) |
| **빌드** | 없음 (단일 HTML) |
| **의존성** | 없음 (Vanilla WebGL) |

### 반응-확산 방정식

두 농도장 A, B가 2D 그리드에서 확산 + 반응:

```
∂A/∂t = Da·∇²A − A·B² + f·(1 − A)
∂B/∂t = Db·∇²B + A·B² − (k + f)·B
```

- `Da`, `Db` — A, B의 확산 계수
- `f` — feed rate (A 보충)
- `k` — kill rate (B 제거)
- `∇²A`, `∇²B` — 5-point Laplacian

`f`와 `k`의 미세한 변화 → 완전히 다른 자기 조직화 패턴 (Turing instability).

---

## 📂 프로젝트 구조

```
gray-scott-reaction-diffusion/
├── index.html      # 단일 HTML (모든 코드 포함 — HTML + CSS + GLSL + JS)
└── README.md       # 한국어 (기본)
```

---

## 🎨 디자인 결정 (Design Choices)

브레인스토밍 단계에서 내린 결정 4가지:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **렌더링 API** | WebGL/GLSL 프래그먼트 셰이더 | CPU JS 대비 100배+ 빠름, 반응-확산은 매 프레임 풀 그리드 계산 필수 |
| **시뮬레이션 패턴** | Ping-Pong FBO (두 텍스처 swap) | GPU에서 시간 단계(dt) 적분 시 표준 패턴, read/write race 방지 |
| **시각화 톤** | 다크 배경 + 화려한 컬러맵(viridis 변형) | 화학 B 농도 변화가 시각적으로 명확, 산호/생물학적 느낌 강조 |
| **인터랙션 깊이** | 마우스 클릭/드래그 + 슬라이더 3종 + 6 프리셋 + 단축키 | "관찰 + 조작 + 탐색" 3단계 모두 지원 |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단에서 다음 상수를 조정하면 분위기를 바꿀 수 있어요:

```js
const CONFIG = {
  GRID_SIZE: 256,           // 시뮬레이션 해상도 (256x256 ~ 512x512)
  STEPS_PER_FRAME: 8,       // 프레임당 시뮬레이션 sub-steps (높을수록 빠름)
  DA: 1.0,                  // A의 확산 계수
  DB: 0.5,                  // B의 확산 계수
  F: 0.062,                 // feed rate (기본: Coral)
  K: 0.062,                 // kill rate (기본: Coral)
  BRUSH_RADIUS: 12,         // 마우스 클릭 주입 범위
  // ... 더 많은 옵션은 코드 내 주석 참조
};
```

고급 사용자용: 프래그먼트 셰이더의 `Laplacian` 커널을 9-point로 확장하거나, 컬러맵 함수를 다른 viridis/plasma로 교체해볼 수도 있어요.

---

## 🗺️ 로드맵 (Roadmap)

- [x] **v0.1** — 단일 HTML MVP: ping-pong 루프, 마우스 시딩, Coral 프리셋
- [x] **v0.2** — 6개 전체 프리셋 + `f`·`k`·브러시 슬라이더 UI
- [x] **v0.3** — Vercel 배포 + 라이브 데모
- [ ] **v0.4** — Record & replay (프레임 시퀀스 → MP4/GIF)
- [ ] **v0.5** — 다중 브러시 모드 (A 주입 / B 주입 / 둘 다 제거 / 정사각형 스플랫)
- [ ] **v0.6** — 3D 두께 슬랩 외삽 (저해상도 복셀 볼륨)
- [ ] **v1.0** — Playwright E2E 테스트 (N프레임 후 패턴 성장 assertion)

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 **MiniMax-M3** 모델과 OpenCode CLI 환경에서 생성되었습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.

- **Gray-Scott 모델**: John Pearson (1993) — *"Complex Patterns in a Simple System"*, Science
- **Ping-Pong 트릭**: GPU Gems / WebGL 커뮤니티 표준 패턴
- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)