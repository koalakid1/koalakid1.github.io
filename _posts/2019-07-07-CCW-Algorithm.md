---
layout: post
title: "CCW(Counterclockwise) 알고리즘 1"
tags: [알고리즘,기하 알고리즘]
use_math: true
comments: true
---

기하 알고리즘의 기초가 되는 **CCW 알고리즘**에 대해 알아보자.

CCW는 Counterclockwise 즉 영어 그대로 해석하면 **반시계 방향**이라는 뜻이다. 

CCW는 PS 중에서도 **선분 교차 여부 판별**을 할때 간단하게 사용하는데 세 점에 대한 방향성을 나타낸다.

CCW의 return은 보통 **3가지 경우**이다.

1. **반시계 방향**
2. **시계 방향**
3. **평행**

이렇게 세가지 경우로 분류가 되고 CCW는 삼각형의 면적을 구하는 공식과 벡터를 이용해서 사용한다.

세 점$$(X_{1}, Y_{1}), (X_{2}, Y_{2}), (X_{3}, Y_{3}) $$이 주어졌을 때, 세 점을 이어서 만든 삼각형의 넓이를 abs(S)라고 하면 다음과 같은 공식이 성립한다.

![_config.yml]({{site.baseurl}}/images/ccw/0707-1.gif)

여기서 S의 부호에 따라서 다음과 같이 세 가지로 나타난다.

* S > 0 : 반시계 방향
* S = 0 : 일직선
* S < 0 : 시계 방향

코드로 나타내면 다음과 같다.

#### C언어

	int CCW(int x1, int y1, int x2, int y2, int x3, int y3) {
    	int temp = x1*y2+x2*y3+x3*y1;
    	temp = temp - y1*x2-y2*x3-y3*x1;
        	return temp
    }

#### 파이썬

	def CCW(x1,y1,x2,y2,x3,y3):
    temp = 0;
        temp += x1*y2+x2*y3+x3*y1;
        temp -= y1*x2-y2*x3-y3*x1;
        return temp

    
그렇다면 이를 이용해서 **어떻게** 선분교차판별을 할 수 있을까?

![_config.yml]({{site.baseurl}}/images/ccw/ccw1.png)

다음과 같은 경우에 **선분 AB**를 기준으로 AB-C와 AB-D가 방향이 다른 것을 알 수 있다. 즉 그 의미는 CCW를 ABC, ABD에 각각 적용했을 때, **부호가 다르다**는 뜻이다.

즉 CCW(A,B,C)와 CCW(A,B,D)의 곱이 음수인 경우, **AB와 CD가 교차**하고 있다는 사실을 알 수 있다.

반대로 평행하는 경우라면 CCW(A,B,C)와 CCW(A,B,D)의 곱이 양수이다.

![_config.yml]({{site.baseurl}}/images/ccw/ccw2.png)

그런데 이 경우를 확인하면 선분 CD에 대해서 CCW(C,D,A)와 CCW(C,D,B)의 부호가 서로 다름에도 불구하고 교차하지 않는 모습을 볼 수 있다.

하지만 선분 AB 입장에서 확인해보면 ABC와 ABD 모두 시계방향이다.

즉 여기서 알 수 있는 사실은 **두 선분을 모두 이용**해서 CCW의 부호를 판별해야 한다는 점이다.

한마디로 CCW(A,B,D)CCW(A,B,C) < 0이고 
CCW(C,D,A)CCW(C,D,B) < 0 이면 두 선분 AB,CD는 교차한다.

관련 문제 - [백준 11758번 CCW](https://www.acmicpc.net/problem/11758)