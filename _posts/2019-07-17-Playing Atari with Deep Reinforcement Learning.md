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

![_config.yml]({{site.baseurl}}/images/dqn/1.PNG)

참고로 t시점의 action에 대한 reward와 state는 t+1시점

###### value function과 q-value function의 차이

value function
어떤 상태 $$s_t$$에서 나는 기대되는 보상이 얼마나 되는지?

Q-value function
어떤 상태 $$s_t$$에서 어떤 행동 $$a_t$$를 취했을 때, 얼마나 좋은 보상이 기대되는지?

###### optimal q-value function

q-value 중에서 가장 최적의 q-value 값을 갖는 q-value function을 의미
$$Q^{*}(s,a)=\max_{\pi }Q^{\pi}(s,a)=Q^{\pi^{*}}(s,a)$$

optimal q-value라는 것은 각각의 상태 s에 대해 행동 action을 정해서 최적의 보상 reward들의 합이다.

그리하여 나오는 것이 bellman equation $$\mathbf{E}_{s'}[r+\gamma \max_{a'}Q^{*}(s',a')|s,a]$$

기존의 q-learning은 table의 형태로 모든 state와 action을 표현했지만 이것은 확장성이 떨어져서 사용이 불가능하기 때문에 q-network를 사용해서 한다. 우리가 가지고 있는 q-network의 결과가 $$Q^{*}$$로 수렴하는 것이 목적이다. (w는 q-network의 parameter)
$$Q(s,a,w)\approx Q^{*}(s,a)$$

bellman equation에서 표현한 q-value를 y, $$Q(s,a,w)$$를 $$y_{predict}$$라고 하면 q-network는 MSE lose를 이용한다.
$$ l = (r + \gamma\max_{a}Q^{*}(s',a',w))^2$$

table방식의 RL에서는 이 방법이 무한히 반복하면 수렴한다는 사실이 있지만 Q-network에서는 아까 전의 이유로 수렴하지 않는다. 그래서 사용한 방법이 바로 experience replay라는 방법이다.