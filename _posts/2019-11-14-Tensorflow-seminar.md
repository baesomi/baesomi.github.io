---
layout: page
title: Tensorflow 2.0 맛보기
tags: Tensorflow2.0
key: page-single
comment: true
comments: true
---

### Tensorflow 2.0
Tensorflow 2.0 이 올해 공개되었는데 Tensorflow 1.0과 비교하여 어떤 점이 달라졌는지 간단하게 요약해보겠습니다.
참고로 이 포스팅은 T Academy에서 실시한 Tensorflow 2.0 - 이진원 님의 강의를 듣고 작성하였습니다.
틀린 부분 있다면 따끔한 지적 해주시면 감사하겠습니다. (강사님은 잘못이없습니다..ㅠㅠ)

### 즉시 실행 (Eager Execution) 모드 

Tensorflow 1.x과 Tensorflow 2.0간 비교를 통해 즉시실행 모드가 무엇인지 알아보자.

![tensorflow-2 0-1](https://user-images.githubusercontent.com/17605895/71509372-67ea3e00-28ce-11ea-8bae-8faa457ce80f.JPG)

기존 Tensorflow 1.x에서는 a,b,c 가 session.run을 통해 수행되기 전까진 실제적인 값이나 의미를 가지지 않는다. 상징적으로 정의한 것일 뿐,
이들은 Session.run이 수행되어 그래프가 생성되었을 때 비로소 제 몫을 한다.
Tensorflow 2.0에서는 session.run 없이 정의 자체로 그 의미를 가진다. 이를 eager execution 이라고 즉시실행이라고 한다. 
현재 머신러닝 분야에서 텐서플로우 다음으로 널리 사용되고 있는 Pytorch에서의 방식과 같다.

더 자세하게 보면    

![tensorflow-2 0-2](https://user-images.githubusercontent.com/17605895/71510113-198a6e80-28d1-11ea-926d-aa9a01d202a9.JPG)

Tensorflow 1.x 에서는 정의한 variable들에 대하여 initializer를 별도로 선언해주어야 하지만, Tensorflow 2.0에서는 우리가 흔히 python 코딩하듯이해주면 끝나는 일이다. 또한 Session.run을 사용하지 않아도 python 코딩하듯이 for문을 돌려주면 실행이 된다. 더불어 debuging이
쉬워진다. 그렇지만 이 즉시실행이 마냥 좋은 것은 아니다. Tensorflow 1.x보다 코딩양이 줄어든만큼 안에서는 수 많은 리소스들을 사용하기 때문에 속도가 느리다는 단점이 있다. 즉시실행에서는 GPU를 사용하지 않고 python을 사용해서 속도가 느리다.



### AutoGraph
![tensorflow-2 0-3](https://user-images.githubusercontent.com/17605895/71510116-1becc880-28d1-11ea-83cb-f851697903f1.JPG)
@tf.function 이라는 데코레이터만 파이썬 함수 위에 추가하면 파이썬 코드를 텐서플로우 코드로 자동 변환해서 속도를 빠르게 할 수 있다.
모든 함수에 적용할 필요는 없으며, simple_func에서 호출된 함수에도 autograph가 적용된다.

### Sequential API
층층이(layer-by-layer) 쌓아 올릴 수 있게 하는 방법으로 대부분의 문제를 해결할 수 있다. 하지만, 이 방법은 layer를 공유하는 구조나, 다중 입력/출력을 사용하지는 못한다는 한계가 있다.


### Functional API
- 독립적인 입력 레이어를 생성
- Layer 재사용가능
- 다중 입출력 값
- 다중 입출력 모델

### Custom Layer


### Custom Model


### 더 알아보기



<!--more-->