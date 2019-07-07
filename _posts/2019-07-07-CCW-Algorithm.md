---
layout: post
title: "CCW(Counterclockwise) 알고리즘"
tags: [알고리즘,기하 알고리즘]
use_math: true
comments: true
---

기하 알고리즘의 기초가 되는 CCW 알고리즘에 대해 알아보자.

CCW는 Counterclockwise 즉 영어 그대로 해석하면 반시계 방향이라는 뜻이다. 

CCW는 PS 중에서도 선분 교차 여부 판별을 할때 간단하게 사용하는데 세 점에 대한 방향성을 나타낸다.

CCW의 return은 보통 3가지 경우이다.

1. 반시계 방향
2. 시계 방향
3. 평행

이렇게 세가지 경우로 분류가 되고 CCW는 삼각형의 면적을 구하는 공식과 벡터를 이용해서 사용한다.

세 점 (X_{1},Y_{1}), (X_{2})

![_config.yml]({{site.baseurl}}/images/0707-1.gif)

