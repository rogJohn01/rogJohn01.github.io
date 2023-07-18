---
layout: post
title:  "leetcode - 2779. Maximum Beauty of an Array After Applying Operation : Java , C++ "
categories: [ ps , leetcode ]
image: assets/images/leetcode_image2.jpg
tags: [featured,leetcode]

---

<br>
### leetcode - 2779. Maximum Beauty of an Array After Applying Operation
[Maximum Beauty of an Array After Applying Operation ](https://leetcode.com/problems/maximum-beauty-of-an-array-after-applying-operation/){:target="_blank"}


---
 

<br><br><br>


\* 이 문제는 weekly-contest 중에 풀지를 못했다. 이후 discussion을 참조해서 다시 정리를 하였다. 
## Logic  


1. 정렬 : 일단 이것은 subarray 가 아닌 subsequence 이기 때문에 순서를 지킬 필요는 없다. 그저 조건만 만족하면 된다. 그렇기 때문에 정렬을 하면 더 문제에 접근하기에 용이하기 때문에 정렬로 먼저 전처리를 한다. 
2. 이 문제는 투 포인터 혹은 슬라이딩 윈도우를 이용해서 풀 수 있다.  
3. 문제의 포인트는 결국 2*k 범위 안에 있는 min-value 와 max-value를 구하는것이다. 이를 위해서 정렬이 유용하고, 투 포인터를 통해서 최적의 구간(정답)을 구할 수 있다. 
4. nums[r]- nums[l] ≤ 2*k조건을 만족하면,  오른쪽 포인터를 계속 움직여준다. 
5. 만약에 위의 조건이 안 맞으면, 왼쪽 포인터를 오른쪽으로움직이면 된다. 이는 왼쪽 구간을 좀 더 오른쪽으로 움직여 구간을 맞추어 주기 위함이다.



```python
class Solution {
    public int maximumBeauty(int[] nums, int k) {
        
        Arrays.sort(nums) ; 
        int l = 0 ; 
        int r ; 
        for(r=0 ; r < nums.length ; r++){
            if( nums[r]- nums[l] > 2*k){
                l ++ ; 
            }
        }
        return r-l ; 
    }
}
```
<br>
### T.C 
O(nlogn)   &nbsp; (정렬)
### S.C
O(1)    &nbsp; (Array를 추가로 사용하지 않는다)
 

<br>
### Edge case 
```python
nums = [1,1,100,100]
```

이러한 경우에도, k=50 이라면 조건이 중족이 된다. 아무래도 포인터를 위해서 array에 있는 값만을 기준으로 삼아서 이렇게 평균값을 써야 되나 하는 케이스에는 통과를 못할 것 같지만, 최솟값에서 + k 그리고 최대값에서 -K 를 해서 즉 최대값 -최소값 <= 2*k 하기 때문에 이러한 케이스에서도 통과가 된다. 

