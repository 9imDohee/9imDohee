---
title: "[Network] OSI 7계층 & TCP/IP 4계층"
excerpt: "Please Do Not Throw Sausage Pizza Away!"

categories:
  - Network   
tags:
  - [네트워크]

permalink: /network/osi-tcpip/

toc: true
toc_sticky: true

date: 2025-09-01
last_modified_at: 2025-09-01
---

## OSI Model (Open Systems Interconnection)

![](https://velog.velcdn.com/images/do_e/post/799d9a68-db78-4c7e-b0f2-26959739b487/image.webp)
[이미지 출처](https://bytebytego.com/guides/top-9-engineering-blog-favorites/)

> <strong>“Please Do Not Throw Sausage Pizza Away”</strong>

| 계층                   | 주요 기능                                               | 예시                               | 데이터 단위                         |
| -------------------- | --------------------------------------------------- | -------------------------------- | ------------------------------ |
| 응용(Application)   | 사용자 애플리케이션과 직접 인터페이스하며, 파일 전송, 이메일, 웹 브라우징 등 서비스 제공 | HTTP, FTP, SMTP, DNS, POP3, IMAP | 데이터(Data)                      |
| 표현(Presentation)  | 데이터 번역, 암호화, 압축 등을 수행하며, 데이터가 사용 가능한 형식인지 보장        | SSL/TLS, JPEG, MPEG, GIF         | 데이터(Data)                      |
| 세션(Session)       | 애플리케이션 간 세션을 설정, 관리, 종료                             | NetBIOS, RPC, PPTP               | 데이터(Data)                      |
| 전송(Transport)     | 신뢰성 있는 데이터 전송, 오류 검사, 흐름 제어 제공                      | TCP, UDP                         | 세그먼트(Segment), 데이터그램(Datagram) |
| 네트워크(Network)     | 데이터 전달 최적 경로 결정, 논리적 주소 지정                          | IP, ICMP, RIP, OSPF              | 패킷(Packet)                     |
| 데이터 링크(Data Link) | 노드 간 전달, 오류 검출 및 수정, 물리적 주소(MAC) 처리                 | Ethernet, PPP, ARP, 스위치          | 프레임(Frame)                     |
| 물리(Physical)      | 물리 매체(케이블, 전파, 광섬유)를 통해 비트 스트림 전송                   | Ethernet 케이블, Wi-Fi, Bluetooth   | 비트(Bit)                        |


<br/>

---




### 1. 물리 계층 (Physical)
 : 컴퓨터 간의 물리적 연결과 신호 전달을 담당하는 계층
 
 #### [주요 특징]
 1. **비트 전송**: 
데이터를 0과 1의 비트 신호(전기, 빛, 전파) 로 변환하여 전송
2. **전송 매체 정의**: 
케이블 종류 UTP, STP, 광케이블, 동축 등
3. **전송 방식 정의**:
단방향/양방향 통신: 단방향(Simplex), 반이중(Half-Duplex), 전이중(Full-Duplex)
4. **속도 제어**: 
데이터 전송 속도(baud rate, bps), 신호 동기화, 클럭 신호 전달
 
#### [e.g.]
케이블, 허브, 리피터: 물리 계층 장비 
컴퓨터 A가 0101 데이터를 보내면, 
물리 계층에서 전압 HIGH/LOW 신호로 변환 → 케이블로 전송 → B의 물리 계층에서 다시 비트로 변환
<br/>

---

### 2. 데이터 링크 계층 (Data Link)
: 신호를 안전하게 전달하고, 누가 데이터를 받을지 관리하는 계층
물리 계층에서 전송된 비트를 프레임 단위로 묶고, 에러 검출/제어, 흐름 제어

#### [주요 특징]
1. **주소지정 (Addressing)**: 
LAN 내 (같은 네트워크 내) 물리적 장치(MAC: Media Access Control) 주소 사용
네트워크 카드의 고유 MAC 주소로 목적지 지정 ⇒ 충돌 방지
    - 접근제어 (Media Access Control, MAC)
    공유 매체(LAN)에서 누가 언제 데이터를 전송할지 결정
    e.g. CSMA/CD, CSMA/CA
    
2. **프레이밍 (Frame)**
0과 1의 단순한 비트를 **프레임(데이터 묶음)** 으로 구분
헤더(Header)와 트레일러(Trailer)를 추가하여 수신측에서 데이터 경계를 인식 가능

3. **에러 검출 및 정정**
전송 중 발생할 수 있는 비트 오류 검출
LLC (Logical Link Control) : 오류 검출, 흐름 제어
e.g. 패리티 비트, CRC(Cyclic Redundancy Check)

4. **흐름 제어 (flow control)**
송신과 수신 속도 차이를 조정
수신측이 처리할 수 있는 속도만큼 데이터 전송

#### [e.g.]
이더넷(유선LAN), Wi-Fi, PPP (Point-to-Point Protocol), 스위치, 브릿지

- 컴퓨터 A가 프레임을 만들고 MAC 주소를 붙여 송신
- 스위치가 목적지 MAC 주소를 확인하여 프레임 전달
- 수신측 컴퓨터 B가 CRC 체크로 에러 여부 확인
<br/>

---

### 3. 네트워크 계층 (Network)  
≒  네이게이션
: 다중 네트워크(서로 다른 네트워크) 간의 경로를 결정하는 계층
논리적 주소(IP) 기반 패킷 전달 및 라우팅
데이터 패킷에 어느 도시, 어느 집( IP 주소) 적음 & 최적 경로 안내 & 길이 막히면 다른 길로 우회 (라우팅 변경)

#### [주요 특징]
1. ** 논리적 주소 지정 (Logical Addressing)**
IP 주소를 사용하여 네트워크 상에서 장치 식별
// MAC 주소는 물리적 주소(Data Link), IP는 논리적 주소(Network)

2. **라우팅(Routing)**
송신자와 수신자가 같은 네트워크에 없을 때 라우터가 중간에서 최적의 경로를 찾아줌
목적지까지 가는 길을 여러 라우터가 협력해서 결정
이동할 경로를 선택하여 Ip 주소를 지정하고, 해당 경로에 따라 패킷을 전달
c.f. 라우터: 서로 다른 네트워크를 연결하고, 패킷의 경로를 결정하는 핵심 장비

3. **패킷 전달(Packet Forwarding)**
데이터 프레임에서 패킷 단위로 분리 → 목적지 주소를 붙여 보냄
패킷은 서로 다른 경로로 가더라도 최종적으로 목적지에서 다시 합쳐짐

**(c.f.)  패킷 단위 스위칭 (Packet Switching)**
- 인터넷: 여러 경로가 존재하는 네트워크의 연결망
- 패킷마다 최적의 경로를 판단해 보낼 수 있기 때문에 같은 출발지 → 목적지 간에도 각 패킷이 다른 경로를 택할 수 있음

4. **분할과 재조립(Fragmentation & Reassembly)**
 큰 패킷을 작은 단위로 나누어 전송 후, **수신 측에서 재조립**

5. **혼잡 제어 & 오류 처리** 
네트워크가 과부하일 때 패킷을 지연시키거나 폐기
ICMP 같은 프로토콜로 오류 메세지 전달 → 핑(ping) 명령, 네트워크 오류 확인
(c.f.) ICMP (Internet Control Message Protocol)
- 네트워크 계층에서 동작하는 제어 및 오류 메세지 프로토콜
- ICMP 메시지는 데이터가 아닌 제어 메시지로, IP 패킷 안에 실려 전송
- IPSec  → 보안 기능(암호화, 인증) 추가

#### [e.g.]
라우터, L3 스위치 (Layer 3 Switch): 스위치 기능 + 라우팅 기능

- 출발지 PC가 목적지 IP를 가진 패킷 생성
- 라우터가 최적 경로를 찾아 패킷 전달
- 중간 네트워크에서 패킷 분할 필요 시 분할 후 전송
- 목적지에서 패킷 재조립 및 상위 계층으로 전달
<br/>

---
### 4. 전송 계층 (Transport)
: 전송계층은 호스트 간 데이터 전송과 애플리케이션 간 통신을 담당

데이터를 **프로세스 간 정확하고 효율적으로 전달**하는 계층

IP 계층에서 받은 패킷을 확인 & 포트 번호로 목적 프로세스 결정 → 데이터를 해당 애플리케이션으로 전달
( c.f.) 프로세스
: 네트워크 통신을 수행하는 애플리케이션 단위

#### [주요 특징]
1. **세그먼트화(Segmentation)**
상위 계층(세션, 애플리케이션)에서 받은 데이터를 세그먼트(Segment) 단위로 쪼갬 
수신 측에서는 이를 다시 합쳐 원본 데이터 복원
* 데이터 단위: 세그먼트(Segment, TCP) / 데이터그램(Datagram, UDP)

2.  **에러 검출 & 신뢰성 보장**
데이터 전송 보장 (재전송, 오류 검출, 순서 보장) 
-  TCP는 신뢰성 제공, UDP는 비신뢰성(빠른 전송)

3. **다중화/역다중화(Multiplexing/Demultiplexing)**
포트 번호 관리 한 장치 안에서도 여러 애플리케이션이 동시에 네트워크를 사용할 수 있음 
포트 번호를 사용해 애플리케이션 구분 
e.g. 브라우저(80/443 포트), 메일(25, 587 포트)

4. **연결 설정과 해제**
TCP는 3-way handshake로 연결을 만들고, 4-way handshake로 연결을 종료

#### [e.g.]
- TCP : 웹 브라우저(HTTP), 이메일(SMTP), 파일 전송(FTP)
- UDP :실시간 스트리밍, 온라인 게임, VoIP
<br/>

---
### 5. 세션 계층 (Session) 
≒  전화
통신을 하는 두 애플리케이션 간의 **대화(세션)**를 관리하는 계층
데이터를 전송할 수 있는 연결을 만들고(Establish), 유지하고(Maintain), 끝내는(Terminate) 일을 담당

#### [주요 특징]
1.  **세션 생성  & 종료**
 두 애플리케이션이 통신할 수 있도록 세션을 열고(Open), 통신이 끝나면 닫음(Close)

2. **동기화 (Synchronization)**
데이터 전송 도중 문제가 생겨도 이어받을 수 있도록 **체크포인트** 설정
대용량 파일 전송 중 끊기면 처음부터가 아니라 중간부터 재개 가능

3. **대화 제어 (Dialog Control)**
통신 방식 관리: 토큰 관리
	- 전이중(Full-duplex): 양쪽이 동시에 송수신 (예: 화상통화)
	- 반이중(Half-duplex): 한 번에 한쪽만 송수신 (예: 무전기)


#### [e.g.]
- 원격 접속(SSH, RPC, NetBIOS)
- 파일 공유 서비스
- 화상 회의(VoIP, Video conferencing)
- 로그인 세션 관리 (예: FTP 로그인/로그아웃)

<br/>

---

### 6. 표현 계층 (Presentation) 
≒  통역사
데이터의 형식을 변환하여 서로 다른 시스템이 이해할 수 있도록 함 (Translation)

#### [주요 특징]
1. **데이터 변환 (Translation)**
서로 다른 인코딩 방식 / 데이터 형식을 맞춤
예: ASCII ↔ EBCDIC, JSON ↔ XML

2. **문법/구문 처리 (Syntax Handling)**
    서로 다른 시스템 간의 데이터 구문 차이를 해결
    
3. **압축과 해제 (Compression/Decompression)**
전송 효율을 높이기 위해 데이터 압축
예: 이미지(JPEG), 동영상(MP4), 텍스트(Gzip)

4. **암호화 및 복호화 (Encryption / Decryption)**
보안을 위해 송신 측에서 데이터를 암호화하고, 수신 측에서 복호화
e.g.  SSL/TLS 암호화 통신


#### [e.g.]
- 파일 형식 변환: JPEG, PNG, GIF, MP4 등
- 데이터 압축: ZIP, GZIP
- 보안 통신: SSL/TLS (HTTPS 기반)
- 문자 인코딩: UTF-8, ASCII, Unicode

<br/>

---
### 7.응용 계층 (Application)
네트워크 서비스를 애플리케이션(프로그램)에 제공하는 계층
사용자가 웹 브라우저, 메일 클라이언트, 메신저 같은 애플리케이션을 통해 네트워크를 이용할 수 있도록 해주는 인터페이스 계층

#### [주요 특징]

1. **네트워크 서비스 제공**
  파일 전송, 이메일, 웹 서비스, 원격 접속 등
2. **사용자 인터페이스 연결**
  사용자가 애플리케이션을 통해 네트워크 기능을 직관적으로 사용 가능
3. **프로토콜 정의**
  애플리케이션 별로 통신 규약(프로토콜)을 제공 → 서비스별 호환성 확보

[e.g.]

- **웹 브라우징**: HTTP, HTTPS
- **이메일**: SMTP, POP3, IMAP
- **파일 전송**: FTP, SFTP, TFTP
- **원격 접속**: SSH, Telnet
- **이름 변환**: DNS
- **네트워크 관리**: SNMP

<br/>

---
## OSI Model & TCP/IP Model
![](https://velog.velcdn.com/images/do_e/post/60547bab-6697-4188-ad1a-3b4f724bc6fb/image.png)
[이미지 출처]( http://rtautomation.com/rtas-blog/a-refresher-course-on-osi-tcp-ip/?srsltid=AfmBOoog-LZsrgVtCM1ppRf4m3pGs_xWKb4WjeKyt_9xqTkThByop1sj)

- **OSI 7계층** → 네트워크 기능을 이론적으로 세분화하여 표준화한 구조 (교육, 표준 설계에 적합)
- **TCP/IP 4계층** → 실제 인터넷 통신에서 쓰이는 구조 (실용적, 단순화)
- 둘의 관계: OSI는 "개념적 모델", TCP/IP는 "구현 모델"



