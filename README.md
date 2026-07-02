# Gray-Scott Reaction-Diffusion Visualization

> **Repo:** [github.com/sigco3111/gray-scott-reaction-diffusion](https://github.com/sigco3111/gray-scott-reaction-diffusion) · **Live:** _add Vercel URL here after OpenCode lands index.html_ · **Built with:** [OpenCode](https://github.com/sst/opencode) + **MiniMax M3**

> Real-time WebGL(GLSL) implementation of the **Gray-Scott reaction-diffusion model** — coral / brain-fold / Turing patterns grow organically across the screen, and you can perturb the chemistry with mouse clicks.

![preview](https://img.shields.io/badge/GLSL-WebGL-ff69b4) ![single--file](https://img.shields.io/badge/single-HTML-blue) ![license](https://img.shields.io/badge/license-MIT-green)

---

## 🤖 How this was built

This project was scaffolded with **[OpenCode](https://github.com/sst/opencode)** using the **MiniMax M3** model.
The full prompt that produced it:

> **Prompt (Korean original)**
>
> 생물학적 패턴을 모방하는 그레이-스콧(Gray-Scott) 반응-확산 알고리즘을 GLSL 쉐이더로 구현하여, 화면 전체에 마치 산호초나 뇌의 주름처럼 복잡하고 유기적인 무늬가 실시간으로 성장하고 변화하는 과정을 시각화하되, 마우스로 클릭하는 지점에 화학 물질을 투입하여 패턴의 흐름을 방해하거나 새로운 무늬를 만들어내는 기능을 넣어줘.
>
> **Implementation Advice**
> WebGL (GLSL) is mandatory for speed here (Reaction-Diffusion is computationally expensive). Use Ping-Pong buffering (swapping two textures) to simulate the time steps of the chemical reaction. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.

The GLSL kernel, ping-pong framebuffer logic, click-to-seed interaction, and UI were all written in one pass by the model — see the commit history for the raw output.

---

## 🚀 Run it

Single-file. No build step. No dependencies.

```bash
# any of these works:
open index.html                # macOS
xdg-open index.html            # Linux
python3 -m http.server 8000    # then visit http://localhost:8000
```

## ✨ Features

- **Pure WebGL/GLSL** — no external libs, runs at 60fps on any modern GPU
- **Ping-Pong buffering** — swaps two textures per simulation step, simulating continuous chemistry
- **Mouse interaction** — click to inject chemical B (or A) and watch the pattern bend / fork / sprout
- **Preset recipes** — classic Gray-Scott parameter pairs (coral, mitosis, spots, worms, …)
- **Drag to paint** — sweep the cursor to inject continuously
- **Pause / reset / randomize** controls

---

## 🧪 Gray-Scott cheatsheet

The model is two concentrations **A** and **B** that diffuse and react on a 2D grid:

```
∂A/∂t = Da·∇²A − A·B² + f·(1 − A)
∂B/∂t = Db·∇²B + A·B² − (k + f)·B
```

| Preset | f (feed) | k (kill) | What you get |
|---|---|---|---|
| Coral | 0.062 | 0.062 | Branching coral fingers |
| Mitosis | 0.0367 | 0.0649 | Cells that split endlessly |
| Spots | 0.035 | 0.065 | Stable round dots |
| Worms | 0.078 | 0.061 | Crawling worms |
| Holes | 0.039 | 0.058 | Swiss-cheese holes |
| Spirals | 0.018 | 0.051 | Slow rotating spirals |

Different `f` / `k` → wildly different morphologies. Try them all.

---

## 📁 Project layout

```
gray-scott-reaction-diffusion/
├── index.html       ← everything: HTML + CSS + GLSL + JS
└── README.md
```

Single-HTML deliverable per the prompt's Implementation Advice. If we later split it out, the natural decomposition would be:

```
index.html
src/
  ├── shaders/
  │   ├── update.frag.glsl   ← ping-pong step
  │   └── render.frag.glsl   ← colormap to screen
  └── js/
      ├── webgl.js           ← context + FBO helpers
      └── presets.js         ← (f, k) table
```

---

## 🗺️ Roadmap

- [ ] **v0.1** — Single-HTML MVP: ping-pong loop, mouse seeding, coral preset ← *current*
- [ ] **v0.2** — Full preset table + UI slider for `f`, `k`, brush size
- [ ] **v0.3** — Record & replay (save frame sequence as a short MP4/GIF)
- [ ] **v0.4** — Multi-seed brush modes (inject A, inject B, kill both, splat square)
- [ ] **v0.5** — 3D thickness slab — extrude the simulation into a low-res voxel volume
- [ ] **v1.0** — Headless E2E test (Playwright) verifying pattern growth over N frames

---

## 📜 License

MIT — see commit history for the AI-assisted origin.

---

# 그레이-스콧 반응-확산 시각화 (한국어)

> **OpenCode + MiniMax M3** 모델로 생성한 단일 HTML 파일 프로젝트.
> 마우스 클릭으로 화학 물질을 투입해 산호초·뇌 주름·튜링 패턴 같은 자기 조직화 무늬를 실시간으로 키울 수 있습니다.

## 실행

```bash
open index.html
```

## 핵심 아이디어

- **그레이-스콧 방정식**을 GLSL 프래그먼트 셰이더에서 픽셀 단위로 계산
- **핑퐁 버퍼링** — 두 텍스처를 번갈아 읽고 쓰며 시간 단계(dt) 시뮬레이션
- **마우스 클릭 / 드래그**로 B(또는 A) 농도를 주입해 패턴 교란

## 프리셋

| 이름 | (f, k) | 모양 |
|---|---|---|
| Coral | (0.062, 0.062) | 산호 가지 |
| Mitosis | (0.0367, 0.0649) | 분열하는 세포 |
| Spots | (0.035, 0.065) | 안정된 점 |
| Worms | (0.078, 0.061) | 기어가는 벌레 |
| Holes | (0.039, 0.058) | 스위스 치즈 |
| Spirals | (0.018, 0.051) | 천천히 도는 나선 |

## 로드맵

- [x] v0.1 — 단일 HTML MVP: 핑퐁 루프, 마우스 시딩, Coral 프리셋
- [ ] v0.2 — 전체 프리셋 + `f`·`k`·브러시 슬라이더 UI
- [ ] v0.3 — 프레임 녹화 → MP4/GIF
- [ ] v0.4 — 다중 브러시 모드 (A 주입 / B 주입 / 둘 다 제거 / 정사각형 스플랫)
- [ ] v0.5 — 두께 슬랩 3D 외삽
- [ ] v1.0 — Playwright E2E 테스트 (N프레임 후 패턴 성장 검증)