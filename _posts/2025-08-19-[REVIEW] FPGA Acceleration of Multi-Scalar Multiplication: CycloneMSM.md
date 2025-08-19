---
title: "[Review] FPGA Acceleration of Multi-Scalar Multiplication: CycloneMSM"
description: "Paper Review about CycloneMSM"
writer: Seongjin Kim
categories: [Paper Review, ZKP Hardware Acceleration]
tags: [Zero-Knowledge Proof, Hardware, Acceleration, FPGA]
image:
  path: ../Images/CycloneMSM_Title.png
  alt: Paper Review about CycloneMSM

math: true
toc: true
toc_sticky: true

date: 2025-07-13
last_modified_at: 2025-07-13
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

<!-- <figure>
  <a href="https://arxiv.org/pdf/2002.08909" class="bookmark source">
    <div class="bookmark-info">
      <div class="bookmark-text">
        <div class="bookmark-title">REALM: Retrieval-Augmented Language Model Pre-Training</div>
        <div class="bookmark-description">arxiv pdf link for REALM</div>
      </div>
    </div>
  </a>
</figure> -->

## 1. Introduction
<center>$$ R = n_{1}P_{1} + n_{2}P_{2} + \cdots + n_{N}P_{N} = \displaystyle\sum_{i=1}^{N} n_{i}P_{i} $$</center>

위 문제를 MSM (Multi-Scalar Multiplication)이라 한다. $$n$$의 경우 255 bit 정도 되며, $$P$$는 타원쌍곡선 위의 점이다. 또한 반복되는 점들의 개수($$ N $$)는 $$ 2^{20} $$ 정도이다. 이러한 많은 큰 값들을 단순히 컴퓨터의 곱셈 연산 처리 방식을 통해 진행한다고 하면, Overhead가 상당해진다.

<img src="../Images/CycloneMSM_1_overhead.png" width = "80%" alt = "fig about MSM Overhead"/>

위의 표를 확인해보면 여러 Scheme(Protocol)에 대해 Prover의 시간에서 MSM이 차지하는 비율이 70-90%를 차지함을 알 수 있다.