---
layout: post
title: "CCW(Counterclockwise) 알고리즘 2"
tags: [알고리즘,기하 알고리즘]
use_math: true
comments: true
---

이번에는 CCW 알고리즘을 활용해서 **다각형의 넓이**를 구해보려고 한다.

물론 다각형이 만약 삼각형과 사각형과 같은 단순하고 기본적인 도형이라면 그 넓이를 구하는 방법은 쉬울 것이다. 하지만 만약 50각형,100각형 등등 N각형의 N이 커졌을 때, 그 넓이를 구하는 방법은 생각보다 힘들다.

그래서 CCW를 이용해서 간단하게 N각형의 도형을 구하는 방법을 설명하겠다.

실제로 우리가 구현할 때 방식은 **4가지 단계**를 거친다.

1. 고정점 한개를 고른다.
2. 고정점을 기준으로 반시계방향으로 2개의 점을 고른 뒤 CCW 코드를 돌린다.
3. 반시계방향으로 모든 점까지 돌려서 그 결과를 누적시킨다.
4. 누적값을 2로 나눈 뒤 절댓값을 씌운다.

간단한 예시와 함께 제대로 설명하자면

![_config.yml]({{ site.baseurl }}/images/ccw/ccw3.png)

위와같은 5각형을 생각해보자. 우선 고정점을 C로 잡으면 반시계 방향으로 D,E를 고를 수 있다. 그리고 CCW를 C,D,E로 돌리면 부호를 상관하지 않고 삼각형의 넓이의 2배가 나올 것이다.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw4.png)

다시 새로 CCW를 돌리기위해 반시계방향으로 한칸 이동하면 D,E에서 E,A로 이동할 것이다. 그러면 다시 C,E,A를 돌려서 CCW의 결과값을 구한다.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw5.png)

마지막으로 남은 CAB까지 돌리면 모든 점을 다 사용해서 CCW의 결과 값을 구하게 된다.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw6.png)

마무리로 총 결과값의 합을 2로 나눈 뒤 절대값을 씌우면 우리가 구하고자하는 5각형의 넓이가 나올 것이다.

그런데 사실 지금의 예시는 모든 3개의 점이 같은 방향을 가지고 있기 때문에 부호를 신경쓰지 않아도 된다. 그렇다면 아래와 같은 경우의 도형은 어떻게 생각해야할까?

![_config.yml]({{ site.baseurl }}/images/ccw/ccw7.png)

이 사진의 경우 고정점을 A라고 했을때 ABC는 시계방향이지만 나머지는 시계 반대방향이다. 일단 우선 규칙대로 CCW를 구하며 진행을 해보자.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw8.png)

처음에는 ABC의 CCW를 구하게 되는데 이렇게 구하면 우리가 원하는 도형의 밖에 위치한 부분을 나타낸다.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw9.png)

그리고 ACD를 하면 처음에 ABC를 한 부분과 겹치는 부분이 생기는데 ABC는 시계방향이고 ACD는 시계 반대방향이기 때문에 겹치는 부분이 상쇄된다. 

![_config.yml]({{ site.baseurl }}/images/ccw/ccw10.png)

그리고 ADE를 구하면 
![_config.yml]({{ site.baseurl }}/images/ccw/ccw11.png)

에서 앞전과 유사하게 겹치는 부분이 서로 반대방향이기 때문에 상쇄된다.

![_config.yml]({{ site.baseurl }}/images/ccw/ccw12.png)

결국에는 우리가 필요한 부분의 결과값만 남게 되기때문에 똑같은 방식으로 도형의 넓이를 구할 수 있게된다.

그러므로 모든 도형에 대해서 이 방식을 사용할 수 있다.

관련문제 - [백준 2166번 다각형의 면적](https://www.acmicpc.net/problem/2166)