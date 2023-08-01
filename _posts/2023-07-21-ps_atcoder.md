---
layout: post
title:  "Atcoder -Contest:ABC-307  D - Mismatched Parentheses  :   Python "
categories: [ ps , atcoder ]
image: assets/images/atcoder1.jpg
tags: [sticky,atcoder]

---

<br>
### contest ABC -307  D - Mismatched Parentheses 
[D - Mismatched Parentheses  ](https://atcoder.jp/contests/abc307/tasks/abc307_d){:target="_blank"}


---
 

<br><br><br>


\* 이 문제는 contest에서 edge cased에 걸려서 풀지 못하고, 다시 edge-case를 찾고 정리해서 풀었다. 앞으로 이러한 문제를 풀 때에는 test case, edge case 를 만드는데 절반 정도의 시간을 투자해 나올 수 있는 parenthses pattern 을 다 커버할 수 있도록 해야 될 것 같다. 
## Logic  
- Stack의 parenthesis 유형은 많은 경우, balance-counter 를 설정하고 활용해주면 문제해결을 쉽게 할 수 있다. balance-counter는 parenthesis 가 몇 개가 open 되고 , closed 되어 있는지를 체크해주는 역할을 한다. 
- 구체적인 로직으로는 parenthesis 는 positive bal 인 경우에만 닫고, 그렇치 않으면 그냥 stack에 담아내는 것이다. 또한 문자열이 가운데 껴 있을 수 있기 때문에 "(" 나올때까지 while문으로 구현을 하면 된다. 

# 풀이

## C++
``` c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main() {
    int N;
    cin >> N;

    string s;
    cin >> s;

    vector<char> st;
    int bal = 0;
    for (int i = 0; i < s.length(); i++) {
        char e = s[i];

        if (e == '(') {
            bal++;
            st.push_back(e);
        } else if (e == ')' && bal > 0) {
            bal--;
            char t = e;
            while (t != '(') {
                t = st.back();
                st.pop_back();
            }
        } else {
            st.push_back(e);
        }
    }

    string ans = "";
    for (char a : st) {
        ans += a;
    }

    cout << ans << endl;

    return 0;
}





```


## Python
```python

N = int(input())
s = input()

st = [] 
bal = 0 
for i in range(len(s)):

    e = s[i]

    if e =="(":
        bal +=1 
        st.append(e)
    elif e ==")" and bal >0: 
        bal -=1 
        t = e 
        while t != "(":
            t = st.pop()
    
    else: 
        st.append(e)


ans =""
for a in st:
    ans +=a 

print(ans)

```
<br>
### T.C 
O(N)  
\: 설령 stack을 뒤에서부터 pop하면서 탐색해도 O(2N) = O(N)
### S.C
O(N)    &nbsp; (Array를 추가로 사용하지 않는다)
 

<br>
### Edge case 
```python

7
ab(a(b)
ab(a

8
ab(a(b)c)
ab

8
ab(()b)
ab

16
ab(a(b)c)ab(a(b)c)
abab

17
ab((a(b)c)ab(a(b)c)
ab(ab

-> found the wc-edge case 
17 
ab(a(b)c)ab(a(b)c))
abab)

-> another one 
ab(a(b)c)ab(a(b)c))()ab

ab(a(b)c)ab(a(b)c))a(b)c 

# main-case 
)(())(



```


