---
layout: post
title:  "baekjoon- 로봇 "
categories: [ ps , baekjoon ]
image: assets/images/baekjoon_image1.jpg
tags: [ps,baekjoon]

---

<br>
[백준 - 로봇 조종하기 ](https://www.acmicpc.net/problem/2169){:target="_blank"}



이 문제는 백준의 욕심쟁이 판다나 백준의 내리막길 문제와 유사해 보인다. 

leetcode에서의 unique path 문제나 rgb거리 같은 문제를 봤을 때에는 

(0,0)에서 시작을 해서 아래쪽 혹은 오른쪽으로만 이동을 해서 (혹은 이렇게 이동해야 만 되는 최단거리 조건을 달아준다) 

일단 처음에는 왼쪽 , 오른족, 아래 세 가지 방향이 가능한데, 

dp는 현재상태의 값이 이전상태 값들의 관걔에 따라 업데이트한데, 

세 가지를 한꺼번에 이용해서 max() 값을 구하는 경우에는 , 최적화가 되지 않는다. 

그 이유는 dp값들을 for-loop으로 순회를 할 때 왼쪽에서 오른쪽으로 이동하게 되면서 왼쪽에서 오른쪽으로 가는 경우는 최신으로 값이 업데이트되어 있지만, 오른쪽에서 왼쪽으로 가는 경우는 값이 업데이트가 되어 있지 않는다. 

이렇기 때문에 , 왼쪽에서 오른쪽 , 그리고 오른쪽에서 왼쪽으로 따로 값을 구한 다음에, 

이 둘을 다시 통합을 해주면 된다. 

통합을 하는 이유 ? 

row을 하나씩 순차적으로 내려가는 데 있어서, 바로 위의 row의 cell이 어떠한 방식으로 내려왔는지는 현재 row는 관심이 없다. 

만약에 이 문제에서 추가적으로 이동경로를 구하라고 한다면 ? 

dp_left[r][c] = [v, path ] → path는 string 으로 해주면 될듯!