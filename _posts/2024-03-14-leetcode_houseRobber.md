---
layout: post
title:  "Leetcode : Houser robber [Top-down]  "
categories: [ ps , leetcode ]
image: assets/images/leetcode_image2.jpg
tags: [featured,leetcode]

---

<br>
### 발상

- 하나의 일관된 규칙으로, 매 순간, 선택/판단-지점마다  단순히 최대가 되는 선택을 추구하는 Greedy 접근방식은  최적값을 가져오지 못한다.
- 왜냐하면, 그 순간에는 최대가 되는 값이 아니더라도, 다음 순간에 최대가 될 수 있기 때문이다. 예를 들어서

```jsx
nums = [ 3,5,100,4] 
```

인 경우에는,  단순하게 첫번째 집과 두 번째 집을 비교해서 두번째 집을 고른다면, 세번째에서 100 만큼의 가치를 선택하지 못하게 된다. 이러한 문제 조건은 Greedy방식으로 최적값을 가져오지 못함을 알 수 있다. 

- 이러한 경우에는 모든 경우의 수를 구하는 완전탐색\백트래킹 방식에 계산의 중복을 없애주는 DP의 메모리제이션 방식을 이용하면 된다.
- 혹은 DP의 보텀업을 이용해서 하나씩 집의 최대값을 타블레이션을 이용해서 접근할 수도 있다.

점화식은 

```jsx
dp[n] = max( dfs(n-2) + nums[n] , dfs(n-1) ) 
```

Top-down방식으로 풀었기 때문에  맨 마지막 집에서부터 시작을 하면 된다. 결국 맨 마지막 집에서는 해당 집을 선택하는 경우 한 집 건너서  두 개 전의 집에서 DP최대값(다양한 경로를 통해서) 과  하나 전의 집에서 DP최대값(다양한 경로를 통해서) 중에서 최대값을 선택해 주면 된다. 

```jsx
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        ln = len(nums)
        dp= [-1]*( ln+1)
      
        def dfs(n): 

            #print("n: " , n )
            if n ==1 or n==0:
                if n==1: 
                    return max(nums[0] ,nums[1])
                else: 
                    return nums[0]

            if dp[n] != -1:
                return dp[n]

            dp[n] = max(dfs(n-2)+nums[n] , dfs(n-1))
            return dp[n]

        return dfs(ln-1)
```

### 시간 | 공간 복잡도

### _Brute-force

- T.C = O(2^N) : 재귀되는 함수가 2개 이므로, 하나씩 집을 탐색할 때마다 두 개씩 경우의 수가 늘어난다.

그러므로 집의 개수만큼 2승을 해주면 된다. 

- S.C = O(1) : 메모리제이션을 이용하지 않기 때문에 최종값만을 저장한다.

### _DP: Top down

- T.C = O(N) : dfs(n-2) & dfs(n-1) 이기 때문에  N ..1 까지 정확히 한 번씩 탐색을 한다. DFS끼리 중복되는 부분은 재귀 되기전에 dp에서 값을 리턴받는다.
- S.C = O(N) :  집 개수만큼 DP 저장공간만큼 필요로 하기 때문에 O(N)이다.

### Edge cases

는 주로  제한조건에서 아이디어를 어느 정도 얻을 수 있다. 

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

문제의 제한조건이 이렇기에 길이가 1이거나 첫번째 항이 0인 값들을 얻을 수 있다. 

```jsx
nums = [0] 

nums = [0,0,0,0,0 .... 0]  |  len(nums) = 400 

nums = [1,2] 

```

- nums 의 원소값이 0이 있을 수 있기 때문에, dp array의 원소값들을 0이 아닌 -1로 세팅할 필요가 있다.