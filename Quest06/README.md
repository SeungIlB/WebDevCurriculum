# Quest 06. 인터넷의 이해

## Introduction
* 이번 퀘스트에서는 인터넷이 어떻게 동작하며, 서버와 클라이언트, 웹 브라우저 등의 역할은 무엇인지 알아보겠습니다.

## Topics
* 서버와 클라이언트, 그리고 웹 브라우저
* 인터넷을 구성하는 여러 가지 프로토콜
  * IP
  * TCP
  * HTTP
* DNS

## Resources
* [OSI 모형](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)
* [IP](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
  * [Online service Traceroute](http://ping.eu/traceroute/)
* [TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
  * [Wireshark](https://www.wireshark.org/download.html)
* [HTTP](https://ko.wikipedia.org/wiki/HTTP)
  * Chrome developer tool, Network tab
* [DNS](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)
  * [Web-based Dig](http://networking.ringofsaturn.com/Tools/dig.php)

## Checklist
* 인터넷은 어떻게 동작하나요? Internet Protocol Suite의 레이어 모델에 입각하여 설명해 보세요.
  → 지역PC가 인터넷에 접근할때 인터넷 영역에서의 수많은 라우팅을 관리하는 Hob(Default Gateway)이 필요하며, 최종적으로 인터넷 사이트에 해당하는 라우터에 접근한다.
  → 보통 상대의 목적지 IP 주소는 특정 값으로 정해지지만, 인터넷의 경우엔 0.0.0.0/0으로 특정지어지지 않는다.
  → 라우팅 경로 정보가 정해져있는 정적라우팅과는 달리, 네트워크 상황에 따라 정보를 빠르게 확보할 수 있는 경로를 중심으로 패킷을 전송하는 라우팅이다.
  → 데이터 정보에 포함된 목적지 주소가 인터넷처럼 광범위하거나, 정적 라우팅을 통한 탐색이 불가능할 경우 동적 라우팅(보통 지역 통신사 등)을 통해 데이터 전달을 진행한다.
  
  * 근거리에서 서로 떨어진 두 전자기기가 유선/무선으로 서로 통신하는 프로토콜은 어떻게 동작할까요?
  → 근거리에 놓여진 두 기기의 네트워크 대역은 보통 정적 라우팅을 통해 연결하며, 라우팅테이블에 저장된 두 기기의 IP와 PORT 정보를 통해 데이터 전달이 이루어진다.
  → 와이파이를 통해 연결한다면 무선 공유기를 통한 라우팅을 진행할 것이고, 블루투를 통해 연결한다면 BLE stack 프로토콜을 기반으로 통신을 진행할 것이다.
  * 근거리에 있는 여러 대의 전자기기가 서로 통신하는 프로토콜은 어떻게 동작할까요?

  * 아주 멀리 떨어져 있는 두 전자기기가 유선/무선으로 서로 통신하는 프로토콜은 어떻게 동작할까요?
  → 사용하는 프로토콜은 두 기기간 거리보다는, 두 기기가 네트워크를 어떤 형태를 통해 연결하였으며 어떤 통신규약을 채용하고 있는지에 영향을 받는다.
  → 보통 멀리 떨어져 있는 기기의 경우엔 근거리 대역의 네트워크가 없어 라우팅 테이블 작성이 어려우므로, 인터넷과 같이 Hob(지역 통신사)를 통한 데이터 전달이 이루어진다.
  
  * 두 전자기기가 신뢰성을 가지고 통신할 수 있도록 하기 위한 프로토콜은 어떻게 동작할까요?
  → 웹과 사용자간의 대표적인 통신규약인 HTTP는, SSL인증을 적용한 HTTPS 프로토콜을 사용한 것이 가장 대표적인 보안적용의 예이다.
  → HTTP프로토콜을 통한 데이터통신 과정에 SSL/TLS 암호화 방식(양방향 암호화)을 적용하여 상대적으로 안전한 데이터 전달이 가능하도록 한 방식이다.
  * HTTP는 어떻게 동작할까요?
  → 웹(서버를 통해 운용되는 HTML 문서)과 사용자 간 정보를 주고받기 위하여 사용하는 통신규약이다.
  → 개발자가 구성한 알고리즘 및 문서구성(HTML)에 따라 데이터 및 헤더에 데이터를 저장하고, request/response를 기반으로 웹사이트 동작이 이루어진다.
* 우리가 브라우저의 주소 창에 www.knowre.com 을 쳤을 때, 어떤 과정을 통해 서버의 IP 주소를 알게 될까요?
1. 사용자가 웹브라우저 검색창에 www.knowre.com 입력
2. 웹브라우저는 캐싱된 DNS 기록들을 통해 해당 도메인주소와 대응하는 IP주소를 확인 이 단계에서 캐싱된 기록에 없을 경우, 다음단계로 넘어간다.
3. 웹브라우저가 HTTP를 사용하여 DNS에게 입력된 도메인 주소를 요청
4. DNS가 웹브라우저에게 찾는 사이트의 IP주소를 응답
ISP(Internet Service Provider)의 DNS서버가 호스팅하고 있는 서버의 IP주소를 찾기 위해 DNS query를 날린다.

## Quest
* tracert(Windows가 아닌 경우 traceroute) 명령을 통해 www.google.com 까지 가는 경로를 찾아 보세요.
  * 어떤 IP주소들이 있나요?
  * 그 IP주소들은 어디에 위치해 있나요?
* Wireshark를 통해 www.google.com 으로 요청을 날렸을 떄 어떤 TCP 패킷이 오가는지 확인해 보세요
  * TCP 패킷을 주고받는 과정은 어떻게 되나요?
  * 각각의 패킷에 어떤 정보들이 담겨 있나요?
* telnet 명령을 통해 http://www.google.com/ URL에 HTTP 요청을 날려 보세요.
  * 어떤 헤더들이 있나요?
  * 그 헤더들은 어떤 역할을 하나요?

## Advanced
* HTTP의 최신 버전인 HTTP/3는 어떤 식으로 구성되어 있을까요?
* TCP/IP 외에 전세계적인 네트워크를 구성하기 위한 다른 방식도 제안된 바 있을까요?
