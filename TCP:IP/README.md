## User Datagram Protocol
DNS

## Transmission Control Protocol
연결설정은 3 way handshake, 연결 설정이 성공해야 데이터를 보낼 수 있다
데이터 전달을 관리하는 규칙
송신사의 포트번호, 수신자의 포트번호, 데이터 순서 번호 등의 정보가 담겨있다

## IP
인터넷 상의 주소 규칙

클라이언트에게 요청이 들어오면 DNS상에서 IP주소를 받아옴 -> HTTP계층에서 HTTP메세지 작성 -> TCP계층에서 패킷으로 분해
-> IP계층에서 전송위치를 확인하고 -> 네트워크를 통해 전송