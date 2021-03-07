---
layout: post
title: VLAN 이란 무엇일까?
subtitle: 패킷트레이서로 보는 VLAN
gh-repo: jaeyoung0826/jaeyoung0826.github.io
gh-badge: [star, fork, follow]
tags: [test, markdown]
comments: true
---

이 글은 한국기술교육대학교 박승철 교수님의 영상과 이경태 강사님의 영상을 토대로 작성하였습니다. 

박승철 교수님 영상:https://www.youtube.com/watch?v=lOZEmfjYIsQ

이경태 강사님 영상:https://www.youtube.com/watch?v=ILv_-eQX7XU

## 서론

최근 네트워크 관련 오픈소스를 보는 중 VLAN 이라는 단어를 많이 들었습니다. VLAN 하면 가상의 LAN이라는 생각이 들기는 하였지만 
그다음 생각나는 부분이 없었습니다. 이에 따라 VLAN의 등장배경과 실제로 어떤식으로 사용되는지 알고자 찾아보고 이를 정리해보았습니다.



## VLAN 정의

우선 VLAN은 Virtual Local Area Network 로 가상 근거리 통신망이라는 뜻입니다. 물리적 배치와 상관없이 LAN을 논리적으로 구성하는 기술을 말합니다.
즉 우리는 Layer 2 에서 네트워크를 나누기 위해서 VLAN을 사용합니다.

## VLAN 의 특징

그렇다면 왜 VLAN 의 특징에는 무엇이 있을까요?


{: .box-note}
**특징 :** 자원의 효율성이 좋아진다!

우선 아래 그림은 VLAN 을 사용하지 않는 환경에서의 네트워크 구성을 표현한 것 입니다.

![그림1](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/76543f3076b39df0d7ae2a49a4b5fb6c4b7c64f0/assets/img/vlan-1.PNG)


그림에서 보면 왼쪽의 Switch 는 sales 서버와 4대의 컴퓨터를, 오른쪽 Switch는 Marketing 서버와 4대의 컴퓨터를 연결되어 있습니다.

이렇게 Switch를 구성하면 통신에는 문제가 없습니다.
하지만 Switch는 24개의 포트를 가지고 있는데 5개의 포트 (4대의 컴퓨터 1대의 서버) 만 사용하고 있으니 19개의 포트는 낭비되는겁니다. 


게다가 이런 Switch가 두개니깐 38개의 포트가 놀고 있고 Switch 수가 증가한다면 자원의 낭비가 더욱더 커지겠죠?
그렇다면 만약 한대의 Switch에 모든 선을 연결한다면 어떨까요? 24개의 포트중 10개의 포트를 사용하니 38만큼의 낭비가 14의 낭비로 줄어드는 효과를 볼 수 있습니다. 

하지만 이는 어디까지 최고의 상황을 말하는거고 실제는 보안상의 문제도 있기 때문에 포트를 남겨서 쓰는일이 많다고 합니다. (포트 수를 줄이기위해 보안이 중요한 서버가 다른 서버와 연결되어서는 안된다는 뜻이죠! )


또한 포트를 모두 사용할때에도 하나의 장비가 통신하려고 하는데 brodcast 방식이라면  23개의 포트에 연결된 장비들도 불필요한 정보를 받아야 하기 때문에 OverHead 가 증가하는 문제가 있습니다. VLAN은 아래에서 살펴볼거지만 특정 VLAN 을 가진 장비들끼리만 통신하므로 불필요한 정보를 받지 않게되는 이점이 생길 수 있습니다.


## VLAN의 동작원리

우선 SWitch 의 VLAN이 전부 1로 설정되어있습니다. (기본 값으로 1로 설정되어있지만 특정회사의 경우 다를 수 있습니다.) 이 VLAN을 포트별로 설정해주면 아래그림과 같이 볼 수 있습니다.

![그림3](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/76543f3076b39df0d7ae2a49a4b5fb6c4b7c64f0/assets/img/vlan-3.jpg)


빨간색 포트는 VLAN 1, 파란색 포트는 VLAN2 로 설정되어있습니다. 

A번 PC에서 프레임을 보내면 Switch를 이를 받고 해당 VLAN정보를 Frame의 tag를 붙혀서 보내줍니다( 사용자의 PC가 아닌Switch 내부에서 할당해주는 것 입니다). 

수신하는 곳에서는 이 프레임 Tag의 VLAN과 자신의 VLAN이 동일한지 확인 후 맞는다면 수신을 받고 아니면 Frame을 받지않습니다.


즉 같은 VLAN을 갖는 Port 끼리만 통신이 가능하다는 것입니다. 이러한 특징 때문에 VLAN을 Port Group 이라고도 합니다.




## 패킷트레이서로 보는 VLAN

아래구조는 앞서 언급하였던 박승철 교수님의 자료를 토대로 구성해본 네트워크입니다. 
![그림4](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/19223207729a22365437212f30dd967cad3355f1/assets/img/%EA%B5%AC%EC%A1%B0.PNG)


VLAN 끼리만 통신 하는 모습을 보여주기 위해 다음과 같은 구성을 만들었는데 빨간색 원이 VLAN 10 
파란색 원이 VLAN 20 입니다. 서버의 경우는 영상에서 다루는 부분이 없기 때문에 지우고 하셔도 무방합니다.

왼쪽 스위치는 각 PC와 Port 1 2 3 4 로 연결했습니다.  IP의 경우 VLAN 10을 사용하는 PC는 192.168.10.X  VLAN 20을 사용하는 PC는 192.168.11.X 로 하였습니다.
Port 5은 서버와 연결되어있으며 서버까지 Packet 전달은 본 글에서는 생략했습니다.

오른쪽 스위츠는 각 PC와 Port 8 9 10 11 로 연결했습니다. Port 1은 서버와 연결되어있으며, Port 24번을 통해 왼쪽 스위치와 연결하였습니다.

IP설정을 다 해준 후에는 Switch 를 클릭하여 CLI 를 사용하여 VLAN을 설정할것입니다.  

1. enable 을 타이핑하여 관리자 모드로 들어갑니다.
2. conf t 를 타이핑하여 terminal로 접근합니다. (conf t -> config terminal)
3. VLAN 10 을 타이핑하여 VLAN 10번을 생성합니다
4. name Marketing 을 타이핑하여 VLAN의 이름을 만들어줍니다. (다른 이름도 괜찮습니다.)
5. exit 를 타이핑하여 다시 config 로 돌아옵니다.
6. 3~5를 반복하여 VLAN 20을 생성해줍니다.


![그림4](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/76543f3076b39df0d7ae2a49a4b5fb6c4b7c64f0/assets/img/vlan-5.PNG)

7. exit를 통해서 treminal 을 빠져나와서 sh vl 을 타이핑하면 아래 그림과 같이 vlan이 설정된것을 확인 할 수 있습니다. (sh vl -> show vlan)


![그림5](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/76543f3076b39df0d7ae2a49a4b5fb6c4b7c64f0/assets/img/vlan-6.PNG)


8. 이제 Port 별로 VLAN을 할당해주기 위해 conf t를 통해 터미널로 접속하고 interface f0/1 를 타이핑해줍니다.
9. interface 로 접속하였으면 switchport access vlan 10 을 타이핑하여 vlan 10 접근권한을 설정해줍니다.
10. exit 로 빠져나옵니다.
11. interface f0/2 을 타이핑하여 똑같은 방법으로 vlan을 설정해줍니다.
12. 같은 방식으로 다른 Port 3,4 의 vlan을 설정해줍니다. (Tip. 연속된 숫자라면 interface range f0/3-x 를 타이핑하여  범위지정이 가능합니다)
13. 오른쪽 스위치도 같은 방법으로 vlan을 생성해주고 각 Port에 할당해줍니다.
14. 마지막으로 Switch 끼리 연결을 위해서 하나의 스위치으 CLI 에 들어가 24번 port의 인터페이스에 들어가서 switchport trunk mode를 타이핑합니다. 


이 과정을 다 하셨으며 위의 서버는 제외하고 Switch 간의 연결은 끝났습니다. 그러면 실제 잘 작동되는지 PC2 에서 PC5으로 Ping을 해보겠습니다.
저 같은경우 PC5의 IP 를 192.168.11.101 로 설정하였으니 PC2의 CMD 에 접속하여 Ping 192.168.11.101 를 사용했습니다.

아래그림을 보면 앞서 특징으로 언급한것과 같이 처음 경로설정시 VLAN 이 다르면 아예 Frame 을 보내지 않아서 OverHead 가 줄어드는 것을 볼 수 있으며 같은 Vlan 끼리 통신이 되고 있음을 알 수 있습니다. (VLAN이 없었다면 PC0과 PC1 에도 Frame 을 수신하는 모습이 생깁니다.) 

![그림6](https://github.com/jaeyoung0826/jaeyoung0826.github.io/blob/19223207729a22365437212f30dd967cad3355f1/assets/img/vlan-10.PNG)

현재는 VLAN 을 대체하는 VXLAN 도 나와있는데 다음 시간에는 이에 대해 다루겠습니다.




