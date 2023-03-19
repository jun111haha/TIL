HTTP(Hyper Text Transfer Protocol) 란 한마디로 HTML(웹문서를 만들기 위한 언어) 문서를 주고 받는데 쓰이는 통신프로토콜(통신규약)이며, 
TCP 와 UDP 를 사용하여 통신하며 80번 포트를 사용하는 통신프로토콜(통신규약)이다.

## google.com을 주소창에 친다면?
1. 브라우저 캐시 체크
- 브라우저는 캐싱된 DNS(Domain Name System) 기록들을 통해 www.google.com 에 대응 되는 IP 주소가 있는지 검색합니다
2. OS 캐쉬 탐색
- 운영체제 안에 있는 systemcall 을 통해 그 내용에 접근하여 찾음
3. 라우터 캐시 확인
- 집에서 사용하는 공유기에서 찾는다 거기서 DNS 탐색을 한다.
4. ISP 캐시 탐색
- 한국에서 인터넷을 제공하는 회사를 생각하면된다

## DNS 로 IP 주소 획득
- ISP 캐시에서까지 ip 주소를 찾을수 없다면 이제 ISP 의 DNS sever 에 DNS 쿼리를 보내야한다. 즉 구글이라는 ip주소 알면 나한테좀 알려줘! 
이를 Revursive search 라고 하는데, 아래의 순서대로 찾는다. 이러한 일은 ISP의 DNS recursor 가 담당하며, 다른 DNS name 서버에다가 물어보는 일을 한다.

![images_doodream_post_3385e8b7-386f-4921-9304-6393fd180573_image](https://user-images.githubusercontent.com/59434443/226158184-ec610f06-2c8f-4ae4-b040-99b3ced83adf.png)

DNS recursor에서 root name server로 연락을 합니다. root name server는 .com 도메인 서버로 접근합니다. .com 도메인 서버는 google.com 도메인 서버로 접근합니다. google.com 네임서버는 www.google.com 에 매칭되는 IP주소를 찾고 DNS recurser로 보내게 됩니다.

이러한 모든 과정은 작은 패킷으로 전달되는 데 이 패킷안에는 DNS query와 DNS recursor의 IP 주소가 포함됩니다. 이러한 패킷이 이동할 때에 Routing table 을 이용하는데 우리가 알고있는 라우터에는 이러한 라우팅 테이블이 있어서 경로 정보를 등록하고 관리해서 최단 경로를 찾을 수 있습니다. 이 패킷들이 중간에 유실되면 request fail error 가 발생하게 됩니다.
