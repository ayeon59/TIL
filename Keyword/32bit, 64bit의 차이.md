# 32 Bit / 64 Bit 차이
##❓❔What is Bit

: 컴퓨터가 정보를 표현하는 가장 작은 단위, 0또는 1로 표현하며 참, 거짓 혹은 서로 배타적인 상태를 나타낸다.

<br>



| 구분          | 32비트                    | 64비트                     |
| ----------- | ----------------------- | ------------------------ |
| **비트 폭**    | 한 번에 처리할 수 있는 데이터가 32비트 | 64비트                     |
| **레지스터 크기** | 32비트 레지스터               | 64비트 레지스터                |
| **주소 공간**   | 최대 4GB 메모리 인식 (2³²)     | 이론상 16EB(엑사바이트) 가능 (2⁶⁴) |


1️⃣ 메모리 한계 <br>
: 고용량 데이터를 처리하는 프로그램은 32bit의 4GB 메모리론 절대 부족하며 에러가 뜨거나 속도가 느려진다.
<br>

2️⃣ 레지스터 크기 차이<br>
: 64bit 레지스터는 더 많은 데이터를 한 번에 처리 가능하며 고속연산에서는 더 큰 단위를 처리할 수 있기 때문에 성능이 향상된다.

3️⃣ 멀티스레드 / 멀티코어 환경<br>
: 64bit OS와 CPU는 더 많은 프로세스와 스레드를 효율적으로 관리하며 대규모 동시 작업에 적합하다.

🔥 32bit는 모든 면에서 이미 한계에 도달했기때문에 확장성과 미래 대응력이 현저히 떨어진다.

다만, 32bit로 만들어진 프로그램들과의 호환성과 저사양 기기 또는 리눅스에서의 경량성을 위해 32bit 또한 필요하다.