# 🧠 비부호형에서의 플래그(flag) 개념

## ✅ 플래그란?
플래그(flag)는 **특정 상태를 0 또는 1의 비트로 나타내는 방법**입니다.  
주로 **여러 개의 상태를 하나의 정수형 변수로 관리**할 때 사용합니다.

예를 들어:
- A 상태 작동 중 → 1  
- B 상태 작동 안함 → 0  
- C 상태 작동 중 → 1

이 세 상태를 한 줄로 표현하면 → `101`  
→ 이진수 `101`은 십진수로 5입니다.

따라서 `unsigned int flags = 0b101;` 같은 식으로 저장 가능!

---

## 💡 비부호형을 사용하는 이유
**비부호형(unsigned)** 정수는 모든 비트를 상태 표현에 사용할 수 있어서 **플래그를 표현할 때 더 효율적**이다.

| 타입       | 사용 가능한 비트 수 | 설명                                 |
|------------|----------------------|--------------------------------------|
| `signed`   | n-1 비트              | 최상위 비트는 부호(MSB)로 사용됨     |
| `unsigned` | n 비트                | **모든 비트**를 상태 플래그로 활용 가능 |

예: `unsigned char` (8비트)  
→ 부호형이면 7비트만 사용 가능 (1비트는 부호)  
→ **비부호형이면 8개의 플래그를 표현 가능!**


## 🛠️ 비트 연산자로 플래그 제어하기

```c
unsigned char flags = 0;      // 모든 상태 꺼짐

// ✔️ 3번째 플래그 켜기 (0부터 시작)
flags |= (1 << 2);

// ❌ 1번째 플래그 끄기
flags &= ~(1 << 1);

// ❓ 2번째 플래그 상태 확인
if (flags & (1 << 2)) {
    // 플래그가 켜져 있음
}
```
##  🛠️ 플래그 상태 제어 예시
```c
#define IS_RUNNING   (1 << 0)
#define IS_VISIBLE   (1 << 1)
#define IS_ERROR     (1 << 2)
#define IS_FINISHED  (1 << 3)

unsigned int flags = 0;

// 상태 설정 
// 해당 상태를 추가
flags |= IS_RUNNING;  // 실행 상태로 전환
flags |= IS_VISIBLE;  // 보이게 설정

// 상태 해제
flags &= ~IS_VISIBLE; // 숨김

// 상태 확인
// flags 가 IS_ERROR 상태라면 0이 될 수 없기 때문에 무조건 실행
if (flags & IS_ERROR) {
    printf("에러 발생!\n");
}
```


## 🧵 Pintos 스레드 상태 관리와 플래그 응용


### ✅ 개요

**스레드(thread)** 는 커널의 작업 단위이며,  
각 스레드는 실행 상태에 따라 관리된다.  

이 상태 정보는 `struct thread` 구조체의 `status` 필드를 통해 추적된다.  
각 상태는 enum으로 정의되지만, 내부 로직에서는 **상태 비교** 및 **전환**을 효율적으로 수행하기 위해 **플래그처럼 다룰 수 있는 구조**를 가진다.


## 📦 스레드 상태(enum 정의)

`threads/thread.h` 파일에 정의된 상태:

```c
enum thread_status {
  THREAD_RUNNING,   // 현재 CPU에서 실행 중인 상태
  THREAD_READY,     // 실행 가능한 상태 (runqueue에 대기)
  THREAD_BLOCKED,   // 이벤트 대기 중 (ex: I/O, lock 등)
  THREAD_DYING      // 종료 대기 중
};

```

```c
#define T_RUNNING   (1 << 0)
#define T_READY     (1 << 1)
#define T_BLOCKED   (1 << 2)
#define T_DYING     (1 << 3)

unsigned int status_flags = 0;

// 상태 설정
status_flags |= T_READY;

// 상태 확인
if (status_flags & T_BLOCKED) {
    // 현재 blocked 상태
}
```





## 🧠 요약 한 줄
"플래그는 다수의 상태를 하나의 변수에 압축해서, 빠르고 효율적으로 관리하는 기법이다."



