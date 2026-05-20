# Results

## 1. 실험 요약
- 저장소: exp-babylon-webgpu-core
- 커밋 해시: 0430345
- 실험 일시: 2026-05-20T15:40:20.234Z -> 2026-05-20T15:40:28.563Z
- 담당자: ai-webgpu-lab
- 실험 유형: `graphics`
- 상태: `success`

## 2. 질문
- Babylon.js 계열 그래픽스 baseline으로 넘기기 전에 scene load와 frame pacing 보고 경로를 먼저 고정할 수 있는가
- material/submesh metadata와 fallback state가 graphics 결과 문서에 같이 남는가
- 실제 Babylon.js WebGPU engine 교체 전 deterministic scene harness로 반복 검증이 가능한가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 32 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: navigator.gpu available
- backend: `webgpu`
- fallback triggered: `false`
- worker mode: `main`
- cache state: `warm`
- required features: ["shader-f16"]
- limits snapshot: {"maxTextureDimension2D":8192,"maxBindGroups":4}

## 4. 워크로드 정의
- 시나리오 이름: Babylon Scene Readiness
- 입력 프로필: 3-meshes-9-submeshes-orbit-camera
- 데이터 크기: meshCount=3; materialCount=3; submeshCount=9; samples=90; backend=webgpu; fallback=false; automation=playwright-chromium, meshCount=3; materialCount=3; submeshCount=9; samples=90; backend=webgpu; fallback=false; realAdapter=fallback(this._adapter.requestAdapterInfo is not a function); automation=playwright-chromium
- dataset: -
- model_id 또는 renderer: babylon-webgpu-core-readiness
- 양자화/정밀도: -
- resolution: 960x540
- context_tokens: -
- output_tokens: -

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 1711.2 ~ 3688.9 ms
- init_ms: 31.1 ~ 31.2 ms
- success_rate: 1
- peak_memory_note: 32 GB reported by browser
- error_type: -

### Graphics / Blackhole
- avg_fps: 56.07 ~ 58.82
- p95_frametime_ms: 17.2 ~ 17.4 ms
- scene_load_ms: 31.1 ~ 31.2 ms
- ray_steps: -
- taa states: undefined
- fallback states: false
- backends: webgpu

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Babylon Scene Readiness | webgpu | warm | 58.82 | 17.2 | scene_load=31.1 ms, fallback=false |
| 2 | Babylon Scene Readiness | webgpu | warm | 56.07 | 17.4 | scene_load=31.2 ms, fallback=false |

## 7. 관찰
- Babylon scene readiness baseline은 backend=webgpu, fallback_triggered=false로 기록됐다.
- graphics summary는 avg_fps=58.82, p95_frametime_ms=17.2, scene_load_ms=31.1였다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. Real Adapter vs Deterministic
- adapter: real=babylon-webgpu-6490, deterministic=deterministic-three-style
- avg_fps: real=56.07, deterministic=58.82, delta=-2.75
- p95_frametime: real=17.4 ms, deterministic=17.2 ms, delta=+0.2 ms
- scene_load_ms: real=31.2 ms, deterministic=31.1 ms, delta=+0.1 ms

## 9. 결론
- Babylon.js 계열 그래픽스 실험으로 넘어가기 전 scene readiness baseline과 결과 문서가 연결됐다.
- 다음 단계는 실제 Babylon.js WebGPU engine을 붙이되 같은 graphics metric 구조를 유지하는 것이다.
- three.js baseline과 같은 capture path를 쓰므로 이후 renderer shootout 입력으로 재사용할 수 있다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-babylon-scene-readiness.png, ./reports/screenshots/02-babylon-webgpu-scene-real-babylon.png
- 로그 파일: ./reports/logs/01-babylon-scene-readiness.log, ./reports/logs/02-babylon-webgpu-scene-real-babylon.log
- raw json: ./reports/raw/01-babylon-scene-readiness.json, ./reports/raw/02-babylon-webgpu-scene-real-babylon.json
- 배포 URL: https://ai-webgpu-lab.github.io/exp-babylon-webgpu-core/
- 관련 이슈/PR: -
