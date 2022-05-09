# DNS와 작동 원리

## 1. DNS란?

우리는 인터넷을 이용하여 검색이나 웹 서핑 , 이메일 등을 사용할 때 도메인 이름(www. Naver. com)을 웹 브라우저의 주소창에 입력하고 네이버에 접속을 합니다. 즉 실제 naver. com 서버는 숫자로 구성된 IP 주소로 통신하지만, 우리는 기억하기 쉬운 도메인 이름을 사용하는 것 그럼 **우리가 입력한 도메인 주소(www. naver .com)를 숫자인 IP 주소로 변환하는 과정이 필요한데 이것을 담당하는 시스템**이 DNS입니다.

## 2. DNS를 사용하는 이유

솔직히 네이버에 접속하기 위해 인터넷창에 곧바로 네이버 IP 주소를 입력하는 사람은 없겠죠? 있다고 해도 그 많은 사이트들의 IP 주소를 일일이 외워서 기억하는 분들은 없을 겁니다. **길고 복잡한 IP 주소를 외울수가 없기 때문에** 문자 주소를 사용하기 위해 DNS를 사용하게 됩니다.

## 3. 구성 요소 및 동작 원리

① **도메인 네임 스페이스 (Domain Name Space)**

: 최상위에 루트 DNS 서버가 존재하고 , 그 하위로 인터넷에 연결된 모든 노드가 연속해서 이어진 계층구조로 구성

② **네임 서버 (Name Server)**

: 주소를 변환 시키기 위해 도메인 네임 스페이스의 트리구조에 대한 정보가 필요. 이 정보를 가진 서버 도메인 이름을 IP주소로 변환하는 것을 네임 서비스

③ **리졸버 (Resolver)**

: DNS클라이언트의 요청을 네임 서버로 전달하고 네임 서버로부터 도메인이름과 IP 주소를 받아 클라이언트에게 제공하는 기능을 수행

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgbNqc%2Fbtq1uuMDN4D%2Fcfifchk6rOn14ZyP9LB8O0%2Fimg.jpg">

도메인 네임은 특정한 순서를 가지고 있습니다.

서비스별 이름이 위치하고 , 조직의 종류 . 국가 이름 순서로 표현됩니다.

Kr : 각 국가별 사용을 위해 정의한 도메인으로 ISO 3166 [4]에서 정의하는 국가 코드에 기반함

com : 기업과 같은 상용 조직을 위한 도메인

edu : 교육 기관들을 위한 도메인

net : 네트워크 서비스 제공자와 관련된 시스템을 위한 도메인

org : 다른 TLD에 속하지 않는 비정부 단체를 위한 도메인

int : 국제 협약에 의해 만들어짂 조직을 위한 도메인

gov : 본래 정부 기관이나 단체를 위한 도메인이었으나, 현재 미국의 주 정부를 비롯한 연방 정부만 등록하도록 결정

mil : 미국 국방성 관련 기관에서 사용하도록 정의한 도메인

arpa : IP 주소를 도메인 이름으로 매핑하기 위해 사용되는 특수 도메인

## ★ DNS 동작과정

<img src="https://velog.velcdn.com/images%2Fgoban%2Fpost%2F5717ceb7-79f2-41d3-86e5-7e48bfd6ac58%2FDNSLogic.png">

1.웹 브라우저에 www.naver.com을 입력하면 먼저 Local DNS에게 "www.naver.com"이라는 hostname"에 대한 IP 주소를 질의하여 Local DNS에 없으면 다른 DNS name 서버 정보를 받음(Root DNS 정보 전달 받음)

### **Root DNS란?**

Root DNS (루트 네임서버) 는 인터넷의 도메인 네임 시스템의 루트 존이다. 루트 존의 레코드의 요청에 직접 응답하고 적절한 최상위 도메인에 대해 권한이 있는 네임 서버 목록을 반환함으로써 다른 요청에 응답한다. 전세계에 961개의 루트 DNS가 운영되고 있다.

2.Root DNS 서버에 "www.naver.com" 질의

3.Root DNS 서버로 부터 "com 도메인"을 관리하는 TLD (Top-Level Domain) 이름 서버 정보 전달 받음 (여기서 TLD는 .com을 관리하는 서버를 칭함)

4.TLD에 "www.naver.com" 질의

5.TLD에서 "name.com" 관리하는 DNS 정보 전달

6."naver.com" 도메인을 관리하는 DNS 서버에 "www.naver.com" 호스트네임에 대한 IP 주소 질의

7.Local DNS 서버에게 "응! www.naver.com에 대한 IP 주소는 222.122.195.6 응답

8.Local DNS는 www.naver.com에 대한 IP 주소를 캐싱을 하고 IP 주소 정보 전달

### **TLD의 구조는 어떻게 구성되어 있을까?**

<img src="https://velog.velcdn.com/images%2Fgoban%2Fpost%2F679d8a2b-1933-4850-95b9-c13765b9ff6c%2FTLD.jpg">

최상위 ICANN 아래에 REGISTRY, NIC이 있고 REGISTRY 아래에 우리가 흔이 보는 gTLD 그리고 new gTLD가 있고 NIC아래에는 공공사이트에서 쓰는 ccTLD 도메인 주소가 있다.

<br><br><br><br><br><br><br><br><br><br><br><br>

1. DNS Query (from Web Browser to Local DNS) : "제가 원하는 웹 사이트의 IP 주소를 알고 계신가요?" Local DNS 서버에게 전달

2. DNS Query (from Local DNS to Root DNS) : "제가 원하는 웹 사이트의 IP 주소를 알고 계신가요?" Root DNS서버에게 전달

3. DNS Response (from Root DNS to Local DNS) : "저는 모르지만 , Com 도메인을 관리하는 네임서버의 이름과 IP 주소를 알려드릴 테니 거기에 물어보세요"

4. DNS Query (from Local DNS to com NS) : “ 안녕하세요. www. naver. com의 IP 주소를 알고 계신가요?"

5. DNS Response (from com NS to Local DNS) : "저는 모르지만 , Com 도메인을 관리하는 네임서버의 이름과 IP 주소를 알려드릴 테니 거기에 물어보세요"

6. DNS Query (from Local DNS to naver. com NS) : “ 안녕하세요. www. Naver .com의 IP 주소를 알고 계신가요?"

7. DNS Response (from naver .com NS to Local DNS) : "저는 모르지만 해당 웹은 www. g.naver. com이라는 이름으로 통해요. g.naver .com 도메인을 관리하는 네임서버의 이름과 IP 주소를 알려드릴테니 거기에 물어보세요"

8. DNS Query (from Local DNS to g.naver. com NS) : “ 안녕하세요. www. g.naver. com의 IP 주소를 알고 계신가요?"

9. DNS Response (from g.naver .com NS to Local DNS) : " 네 www. g.naver .com의 IP 주소는 222.222.222.22와 333.333.333.33입니다"

10. DNS Response (from Local DNS to Web Browser) : "네 www. naver .com의 IP 주소는 222.222.222.22와 333.333.333.33입니다"
