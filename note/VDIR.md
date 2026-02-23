# Variational Deep Image Restoration (VDIR) – Summary

## 1. 문제 상황

최근 Image Restoration 분야에서는 CNN 기반 모델이 많이 사용되고 있다.  
일반적으로 noise image(y)를 입력으로 받아, clean image(x)를 바로 예측하는 방식이다.    
하지만 real-world degradation은 단순하지 않은데, 이유는 다음과 같다.

- blur의 원인이 여러 가지일 수 있고
- noise의 형태도 다양하며
- 하나의 손상 이미지에 대해 여러 개의 가능한 정답이 존재할 수 있다.

기존 모델은 보통 하나의 정답만을 예측하도록 학습되기 때문에,
이러한 **multi-modal degradation**을 잘 표현하지 못한다.

이 논문은 이 문제를 해결하기 위해,
image restoration을 **probabilistic**으로 다루는 방법을 제안한다.

---

## 2. 기존 방법의 한계

기존 CNN restoration model의 특징은 다음과 같다:

- L1 또는 L2 loss를 사용
- 하나의 출력 이미지만 생성
- 평균적인 결과를 만드는 경향이 있음


이 방식은 손상 원인이 명확할 때는 잘 동작한지만, real-world에서 아래와 같은 한계를 갖는다:

- 같은 입력 이미지에 대해 여러 개의 restoration이 가능
- noise나 blur가 복합적으로 섞여 있음
- degradation matrix가 정확히 알려져 있지 않음


---

## 3. 논문의 핵심 아이디어

이 논문은 image restoration을 단순한 regression 문제가 아니라,
**확률 분포를 학습하는 문제**로 접근한다.

즉,

- "하나의 정답 이미지를 맞추는 것"이 아니라
- "가능한 여러 복원 결과를 표현하는 것"을 목표로 한다.

이를 위해 아래와 같은 방법을 적용한다:

- latent variable(잠재 변수)를 도입
- variational inference 기반 구조 사용
- 복원 결과를 확률적으로 모델링

다시 말하자면,
손상 이미지 y가 주어졌을 때,
깨끗한 이미지 x를 하나로 고정하지 않고,
**가능한 여러 결과를 생성할 수 있도록 학습하는 것**이다.

---

## 4. 모델 구조 개념

VDIR은 크게 두 부분으로 이해할 수 있다.

### (1) 인코더(Encoder)

- 손상 이미지와 깨끗한 이미지를 함께 입력으로 사용
- latent variable을 학습

### (2) 디코더(Decoder)

- 손상 이미지와 latent variable을 함께 입력
- 복원 이미지 생성

이 구조를 통해,
같은 입력 이미지에 대해서도
latent variable 값을 다르게 설정하면
서로 다른 복원 결과를 얻을 수 있다.

---

## 5. 실험 결과 요약

논문에서는 다음을 보여준다:

- 기존 deterministic 모델보다
  real-world degradation 상황에서 더 robust
- 단일 출력이 아닌, 다양한 복원 결과 생성 가능
- 복잡한 손상 환경에서 더 자연스러운 결과 생성

특히,
손상 원인이 명확하지 않은 경우에
probabilistic 접근이 더 적합함.

---

## 6. 이 논문의 의미

이 논문은 이미지 복원을 다음과 같이 다시 정의한다:

- 단순한 input-output mapping 문제가 아님
- uncertainty을 포함한 문제
- 여러 가능한 restoration 결과를 고려해야 하는 문제

기존 CNN 기반 image restoration이 “평균적인 답”을 찾는 방식이었다면,
VDIR은 “가능한 답의 분포”를 학습하려는 시도라고 볼 수 있다.