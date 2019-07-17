---
layout: post
title: "Playing Atari with Deep Reinforcement Learning"
tags: [알고리즘,그래프]
use_math: true
comments: true
---
### Playing Atari with Deep Reinforcement Learning

논문 링크 - [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/pdf/1312.5602.pdf)

위 논문은 Deepmind가 2013년도에 NIPS workshop에서 발표한 논문이다.

RL을 적용할때 많은 사람들이 high dimensional sensory input을 직접 사용하고 싶었지만 이때까지 너무 방대한 양이라서 직접 사용하는건 불가했고 이는 결국 확장성의 문제까지 왔기 때문에 사실상 침체기였다.

그런데 이 시기에 deep learning 논문이 나왔고 이를 RL을 적용해보기위해 사용해봤지만 실제로 RL에서는 크게 2가지의 이유로 사용할 수 없었다.

1. test 데이터의 labeling이 되어있지 않는다.
2. DL의 data sample들은 서로 independent해야하지만 RL은 correlated state들의 sequences들로 이루어져있다.

그래서 실제로 DL을 적용해본 팀이 있기는 하지만 성공하지 못했다. 그런데 deepmind에서는 각각의 이유에 대한 해결방안을 고려해서 이를 가능하게 했다. 

1. CNN을 수정된 Q-learning 활용해서 해결
2. Experience replay를 활용해서 해결

#### notation

![_config.yml]({{site.baseurl}}/images/dqn/1.png)

###### value function과 q-value function의 차이

value function
어떤 상태 &&s_t&&에서 나는 기대되는 보상이 얼마나 되는지?

Q-value function
어떤 상태 &&s_t&&에서 어떤 행동 &&a_t&&를 취했을 때, 얼마나 좋은 보상이 기대되는지?

###### optimal q-value function

q-value 중에서 가장 최적의 q-value 값을 갖는 q-value function을 의미
&&Q^{*}(s,a)=\max_{\pi }Q^{\pi}(s,a)=Q^{\pi^{*}}(s,a)&&