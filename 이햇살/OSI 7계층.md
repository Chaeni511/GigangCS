# OSI 7계층

> OSI(Open System Interconnection) 7계층은 국제 표준화 기구인 ISO(International Standardization Organization)에서 개발한 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 개방형 시스템 상호 연결 모델

<img src="C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813231323213.png" alt="image-20230813231323213" style="zoom: 70%;" />

```null
AH : Application Header
PH : Presentation Header
SH : Session Header
TH : Transport Header
NH : Network Header / NT : Network Tail
DH : Data Link Header / DT : Data Link Tail

계층을 지날 때 마다 헤더(Header)가 붙는데, 이것은 해당 계층의 기능과 관련된 제어 정보가 포함 되어 있다.
제어 정보들을 모두 운영체제가 제공하는 프로토콜에 의해 송신 측에서는 계층을 지날 때마다 덧붙여서 추가되고, 수신 측에서는 계층을 지날 때마다 제거된다.
```

![img](https://velog.velcdn.com/images/genius_jihyepark/post/1da3b406-d521-46c3-b2b4-50edc6473dae/image.png)

## 1. 물리 계층 (Physical Layer)

> 물리계층은 실제 장치들을 연결하기 위해 필요한 전기적,물리적 세부 사항들을 정의하는 계층 
>
> 통신 채널을 통해 전송되는 사용자 장치의 디지털 데이터를 이에 상응하는 신호들로 변환
>
> - 프로토콜 : RS-232
>
> - 단위: **Bit** 비트
> - 장비 : 리피터, 케이블, 허브 등

![image-20230813231501721](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813231501721.png)

- 데이터를 전기적인 신호(0,1비트)로 변환하여 주고받는 공간
- 데이터를 전송하는 역할만 함

- OSI 계층을 타고 전달된 데이터를 전기적인 신호(Bit)로 변환시켜 통신을 수행.
- 데이터 링크 개체 간의 비트 전송을 위한 물리적 연결을 설정, 유지, 해제 하기 위한 수단을 제공

## 2. 데이터 링크 계층 (Data Link Layer)

> 데이터 링크 계층은 링크의 설정과 유지 및 종료를 담당하며 노드 간의 오류제어, 흐름제어, 회선제어 기능을 수행하는 계층
>
> 네트워크 계층에 데이터를 전달하고, 물리 계층에서 발생할 수 있는 오류를 탐지하고 수정하는 기능을 제공
>
> - 프로토콜 : HDLC, PPP, 프레임 릴레이, ATM
> - 장비 : 스위치(Switch),  브리지(Bridge)
>
> - 단위: **Frame** 프레임

![image-20230813231831790](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813231831790.png)

- 물리 계층으로 송수신되는 정보를 관리하여 안전하게 전달
- Mac 주소를 통해 통신
- Frame에 Mac 주소를 부여하고 에러검출, 재전송, 흐름제어 진행
  - Mac주소 (Media Access Control)
    - 컴퓨터의 고유한 주소
    - 컴퓨터 간 데이터를 전송하기 위해 있는 컴퓨터의 물리적 주소 또는 하드웨어 주소

- 시스템 간에 오류 없는 데이터 전송을 위해 상위 계층에서 받은 패킷을 프레임으로 변환하여 물리계층으로 전송
- 헤더의 끝에는 물리 주소 정보가 들어있고, 트레일러에는 오류를 검출하는 비트 포함

## 3. 네트워크 계층 (Network Layer)

> 네트워크 계층은 다양한 길이의 패킷을 네트워크들을 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 위한 수단을 제공하는 계층
>
> 라우팅, 패킷 포워딩, 인터 네트워킹 등을 수행
>
> - 프로토콜 : IP, ARP, RARP, ICMP, IGMP, 라우팅 프로토콜
> - 장비 : 라우터(Router), L3 스위치, IP 등
> - 단위: **Packet** 패킷
>   - 전달 해야하는 데이터는 출발지 정보, 목적지 정보가 부가적으로 필요하며 해당 정보는 IP로 처리하고, IP정보를 붙인 데이터를 패킷이라고 함

![image-20230813232823346](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813232823346.png)

- 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능(라우팅)을 담당
- 라우터를 통해 이동할 경로를 선택하여 IP 주소를 지정하고, 해당 경로에 따라 패킷을 전달해준다.

- 패킷을 네트워크를 통해 발신지에서 목적지까지 전달하기 위해, 라우팅 프로토콜을 사용하여 최적의 경로 선택
- 데이터를 전송할 데이터의 주소 확인 후 전송 계층으로 전달

## 4. 전송 계층 (Transport Layer)

> 전송 계층은 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해주면서 종단 간의 사용자들에게 신뢰성 있는 데이터를 전달하는 계층
>
> 순차번호 기반의 오류 제어 방식을 사용하고, 종단 간 통신을 다루는 최하위 계층으로 종단 간 신뢰성 있고 효율적인 데이터를 전송
>
> - 프로토콜 : TCP, UDP
> - 장비 : L4 스위치, 게이트웨이
> - 단위: TCP - Segment / UDP - Datagram

![image-20230813232939805](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813232939805.png)

- TCP와 UDP 프로토콜을 통해 통신을 활성화
  - 포트를 열어두고, 프로그램들이 전송을 할 수 있도록 제공

- TCP : 신뢰성, 연결지향적
- UDP : 비신뢰성, 비연결성, 실시간

- 사용자들이 신뢰성있는 데이터를 주고 받을 수 있게 해주며, 패킷들의 전송이 유효한 지 확인하고 전송 실패한 패킷들을 다시 전송

## 5. 세션 계층 (Session Layer)

> 세션 계층은 응용 프로그램 간의 대화를 유지하기 위한 구조를 제공하고, 이를 처리하기 위해 프로세스들의 논리적인 연결을 담당하는 계층
>
> 통신 중 연결이 끊어지지 않도록 유지시켜주는 역할 수행하기 위해 TCP/IP 세션 연결의 설정과 해제, 세션 메세지 전송 등의 기능을 수행
>
> - 프로토콜 : PRC, NetBIOS, SSH, TLS
> - API, Socket
>
> - 단위: Data / Message(Token)

![image-20230813233334055](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813233334055.png)

- 데이터가 통신하기 위한 **논리적 연결**을 담당
  - 네트워크 상 양쪽 연결을 관리하고 연결을 지속 시켜 주는 계층

- TCP/IP 세션을 만들고 없애는 책임을 지고 있음
  - 통신하는 사용자들을 동기화한다는 특징

## 6. 표현 계층(Presentation Layer)

> 표현 계층은 애플리 케이션이 다루는 정보를 통신에 알맞은 형태로 만들거나, 하위 계층에서 온 데이터를 사용자가 이해할 수 있는 형태로 만드는 역할을 담당하는 계층
>
> 수신자 장치에서 적합한 애플리케이션을 사용하여 응용계층 데이터의 부호화 및 변환 수행을 통해 송신 장치로부터 온 데이터를 해석
>
> - 프로토콜 : JPEG, MPEG, SMB, AFP
> - 단위 : Message

![image-20230813233936152](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813233936152.png)

- 데이터 표현에 대한 독립성을 제공하고 암호화하는 역할을 담당
  - 코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식 상 차이를 다루는 부담을 응용 계층으로부터 덜어 줌

- 파일 인코딩, 명령어를 포장, 압축, 암호화

  ex) 특정 데이터의 형식이 text인지, gif, jpg인지 등의 구분, EBCDID로 인코딩된 문서 파일을 ASCII로 인코딩된 파일로 바꿔주는 것 등

## 7. 응용 계층(Application Layer)

> 응용 계층은 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행하는 역할을 담당하는 계층
>
> 응용 프로세스가 개방된 형태로 다양한 범주의 정보처리기능을 수행할 수 있도록 여러가지 프로토콜 개체에 대하여 사용자 인터페이스를 제공
>
> - 프로토콜 : HTTP, FTP, DNS 등
> - 장비 : L7 스위치
> - 단위: Data

![image-20230813234103634](C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230813234103634.png)

- 최종 목적지로, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행
- 응용 프로세스 간의 정보 교환, 파일 전송 등의 서비스를 제공

- 사용자 인터페이스, 전자우편, 데이터베이스 관리 등의 서비스를 제공

---

참고자료

[[CS면접_네트워크] OSI 7 계층](https://velog.io/@genius_jihyepark/CS%EB%A9%B4%EC%A0%91%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5)

[[네트워크] OSI 7 계층 개념 정리](https://velog.io/@poiuyy0420/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)

