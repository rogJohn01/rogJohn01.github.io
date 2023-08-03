---
layout: post
title:  "지식: Reverse Proxy vs Forward Proxy "
categories: [Knowledge , Project]
image: assets/images/reverse_proxy.jpg
tags: [Knowledge , Project]

---

<br>

### 프록시(proxy)란 ? 
서버와 클라이언트 사이의 가상의 서버를 만들어 대리 서버 역할을 해주는 것을 프록시 서버라고 한다. 

### 리버스 프록시(Reverse proxy)
리버스 프록시(Reverse proxy)란 서버 차원에서 서버 앞에 프록시 서버를 배치해 서버에 요청이 오는 것들을 먼저 프록시 서버를 경유해 서버 컴퓨터에 전달을 하는 구조이다.  

리버스 프록시는 여러 가지 용도 및 특징이 있지만, 주로 Load-balancing을 할 때 쓴다. Load-balancing을 하기 위해서는 먼저 요청을 받아서  여러개의  웹서버에 분배해주는 상단의 서버가 필요한데 이것이 리버스 프록시(서버) 이다.  물론 이러한 load-balancing 서버 또한 큰 트래픽이 올 때 서버가 다운 될 수 있는 데  이것을 단일 장애 지점(Single point of failure) 라고 한다. 이러한 단일 장애 지점에 대한 해결책은 load-balancing 서버를 하나가 아닌 여러개를 구축하는 것이다. 

load-balancing 이외의 리버스 프록시의 특징은 

- 서버측 보안(securtiy) :  클라이언트 쪽에서는 실제 웹서버의 ip주소 및 url을 알지 못한다.
- 캐싱(caching) :  이미 요청이 된 데이터는 다시 웹서버에 있는 DB까지 가지 않고, 리버스 프록시 서버가 처리를 한다.
- 암호화 (Encryption) : 리버스 프록시를 사용하게 되면 , SSL 암호화 , 복호화 비용을 줄일 수 있다.

실제로 리버스 프록시를 구축할 때에는 Nginx을 주로 사용을 한다. 물론 apache HTTP server 를 이용해도 되고, AWS Elastic Load Balancer (ELB) or AWS CloudFront 와 같은 클라우드 서비스슬 이용할 수도 있다.


![Example Image](/assets/images/reverse_proxy2.jpg){: width="700" height="500"}


## 포워드 프록시란 :

리버스 프록시가 웹서버 앞의 프록시 서버를 구축하는 것이었다면, 포위드 프록시 서버는 클라이언트 앞에 프록시 서버를 구축하는 것이다. 

포위드 프록시의 주 용도는 웹 사이트 제한으로 볼 수 있다. 

특징 : 

- 특정 사이트 제한 :
- 클라이언트 익명성 : 클라이언트가 프록시 서버를 통해서 서버에 접속이 되기 때문에 , 서버는 클라이언트의 ip주소를 알 수 없다.  그렇기 때문에 익명으로 웹서버에 접속할 수 있다.
- 캐싱 : 같은 네트워크 안에 있는 다른 사용자가 이미 데이터를 요청해 포위드 프록시 서버에 저장되어 있는 데이터가 있다면, 포위드 프록시 서버가 캐싱 역할을 해준다.

<br>
<br>

![Example Image](/assets/images/reverse_proxy.jpg){: width="700" height="500"}
