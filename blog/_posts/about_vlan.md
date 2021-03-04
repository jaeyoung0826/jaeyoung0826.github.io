---
layout: post
title: VLAN 이란 무엇일까?
subtitle: 패킷트레이서로 보는 VLAN
gh-repo: seokho-son/seokho-son.github.io
gh-badge: [star, fork, follow]
tags: [test, markdown]
comments: true
---

이 글은 한국기술교육대학교 박승철 교수님의 영상을 토대로 썼습니다. https://www.youtube.com/watch?v=lOZEmfjYIsQ


## 서론

최근 네트워크 관련 오픈소스를 보는 중 VLAN 이라는 단어를 많이 들었습니다. VLAN 하면 가상의 LAN이라는 생각이 들기는 하였지만 
그다음 생각나는 부분이 없었습니다. 이에 따라 VLAN의 등장배경과 실제로 어떤식으로 사용되는지 알고자 찾아보고 이를 정리해보았습니다.



## VLAN 정의

우선 VLAN은 Virtual Local Area Network 로 가상 근거리 통신망이라는 뜻입니다. 물리적 배치와 상관없이 LAN을 논리적으로 구성하는 기술을 말합니다.


## VLAN 의 이점

그렇다면 왜 LAN을 논리적으로 구성하면 어떤 이점이 있기 때문에 VLAN이라는 기술을 사용하게 되었을까요? 


{: .box-note}
**이점 :** 자원의 효율성이 좋아진다!

우선 아래 그림은 VLAN 을 사용하지 않는 환경에서의 네트워크 구성을 표현한 것 입니다.

![그림1]()


그림에서 보면 왼쪽의 Switch 는 sales 서버와 4대의 컴퓨터를, 오른쪽 Switch는 Marketing 서버와 4대의 컴퓨터를 연결되어 있습니다. 이렇게 Switch를 구성하면 통신에는 문제가 없습니다.
하지만 Switch는 24개의 포트를 가지고 있는데 5개의 포트 (4대의 컴퓨터 1대의 서버) 만 사용하고 있으니 19개의 포트는 낭비되는겁니다. 
게다가 이런 Switch가 두개니깐 38개의 포트가 놀고 있고 Switch 수가 증가한다면 자원의 낭비가 더욱더 커지겠죠?
그렇다면 만약 한대의 Switch에 모든 선을 연결한다면 어떨까요? 24개의 포트중 10개의 포트를 사용하니 38만큼의 낭비가 14의 낭비로 줄어드는 효과를 볼 수 있습니다. 


## VLAN의 동작

작성중

