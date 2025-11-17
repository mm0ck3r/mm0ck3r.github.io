---
title: "[Paper Review] cuZK: Accelerating Zero-Knowledge Proof with A Faster Parallel Multi-Scalar Multiplication Algorithm on GPUs"
description: "Paper Review about cuZK"
writer: Seongjin Kim
categories: [Paper Review, ZKP Hardware Acceleration]
tags: [Zero-Knowledge Proof, Hardware, Acceleration, GPU]
image:
  path: ../Images/cuZK/Title.png
  alt: Paper Review about CycloneMSM

math: true
toc: true
toc_sticky: true

date: 2025-10-02
last_modified_at: 2025-10-15
---

<style>

img {
  display: block;
  margin: auto;
}

  figure {
	margin: 1.25em 0;
	page-break-inside: avoid;
}
.bookmark {
	text-decoration: none;
	max-height: 8em;
	padding: 0;
	display: flex;
	width: 100%;
	align-items: stretch;
}

.bookmark-title {
	font-size: 0.85em;
	overflow: hidden;
	text-overflow: ellipsis;
	height: 1.75em;
	white-space: nowrap;
}

.bookmark-text {
	display: flex;
	flex-direction: column;
}

.bookmark-info {
	flex: 4 1 180px;
	padding: 12px 14px 14px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.bookmark-description {
	color: rgba(167, 172, 172, 1);
	font-size: 0.75em;
	overflow: hidden;
	max-height: 4.5em;
	word-break: break-word;
}

.bookmark-href {
	font-size: 0.75em;
	margin-top: 0.25em;
}
</style>

```MSM GPU Acceleration```에 관해 기본적인 내용들을 학습하기 좋은 것 같아 ```cuZK``` 논문을 리뷰해보도록 하겠다. 
MSM(Multi-Scalar Multiplication)에 대해 자세히 알고싶으면 이전 [포스팅](https://mm0ck3r.github.io/posts/REVIEW-cuZK-Accelerating-Zero-Knowledge-Proof-with-A-Faster-Parallel-Multi-Scalar-Multiplication-Algorithm-on-GPUs/)을 참조하자.

# 1. Introduction
```Groth16```의 ZK-SNARKs에 의해 ZKP 과정은 매우 간결해지게 되었다. 
다만, Prover가 증명을 생성하는 단계에서는 아직 overhead가 크다는 단점이 존재한다. 

증명자가 증명 $$ -\pi $$를 생성하려면,