[English](./README.md) | [한국어](./README.ko.md)

# SuperPower-Up

[Superpowers](https://github.com/obra/superpowers) 잘 쓰고 있는데, 쓰다 보니 조금 더 욕심이 생겼습니다.

좋은 스킬도 많고, 쓸 만한 도구도 많은데 이걸 Superpowers와 잘 엮어서 쓰면 더 좋지 않을까?

그래서 이것저것 붙여보고, 조합해보고, 마음에 안 들면 다시 뜯어고치는 중입니다.

Superpowers의 워크플로우를 기반으로 필요한 기능은 보강하고, 중복되거나 불필요한 복잡함은 줄여보려고 합니다.

**목표는 나름 잘 굴러가는 코딩 하네스 만들기.**

## 현재 구상

```text
Research
   │  기술 조사 · 대안 탐색
   ▼
Requirements
   │  요구사항 · 설계 결정
   ▼
Development
   │  Superpowers
   │  ├─ Spike
   │  ├─ Bounded
   │  └─ Architectural
   ▼
Final Quality
   │  코드 단순화
   │  독립 리뷰
   │  최종 검증
   ▼
Done!
```

각 단계는 사용자가 직접 시작합니다. Superpowers는 개발 워크플로우의 중심을 맡고, 나머지는 필요한 스킬과 도구들로 보강하는 방식입니다.

**보조 도구 및 스킬**

- **Matt Pocock Skills** — 리서치, 요구사항, 설계, 리뷰
- **Graphify** — 코드베이스 탐색 및 영향 분석
- **Context7 / GitHub MCP** — 라이브러리 문서와 외부 코드 참고
- **NVIDIA Skills** — NVIDIA 관련 개발 지원
- **Karpathy Guidelines / Code Simplifier** — 구현 원칙과 코드 정리

전부 매번 쓰는 건 아니고, 필요할 때 필요한 것만 꺼내 쓰는 게 목표입니다.

## 현재 상태

아직은 [`CLAUDE.md`](./CLAUDE.md) 파일 하나.

아이디어는 많은데 구현은 이제 시작입니다.

구조도, 도구 조합도, 워크플로우도 계속 바뀔 수 있습니다.
