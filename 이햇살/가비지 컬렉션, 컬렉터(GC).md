# 가비지 컬렉션, 컬렉터(GC)

## 1. 가비지 컬렉션(Garbage Collection)

### 1.1 정의

- 쓰레기(가비지)를 정리해주는 프로그램
- 시스템에서 더 이상 사용하지 않는 동적 할당된 메모리 블록이나 객체를 찾아 자동적으로 다시 사용 가능한 자원으로 회수

 ### 1.2 가비지 컬렉션 실행시점

- JVM이 메모리가 부족해지면 OS에 추가로 메모리 요청을 할 때 가비지 컬렉션이 실행

 ### 1.3 가비지 컬렉션 알고리즘

- `마킹 작업` : 사용중인 메모리와 사용하지 않는 메모리 식별
- `일반 삭제` : 참조되지 않는 객체를 제거하고 빈 공간에 대한 포인터를 남긴다.

### 1.4 가비지 컬렉터(Garbage Collector) 종류

- Serial GC : MinorGC, MajorGC를 순차적으로 진행
- Parallel GC : 여러 CPU를 효과적으로 활용하기 위해 GC 수행시 멀티쓰레드를 사용
- CMS Collector : 가비지 컬렉션 작업을 어플리케이션 쓰레드와 동시 수행하여 Stop the World 시간을 최소화
- G1 Garbage Collector : 여러 CPU와 아주 큰 Memory에서 효과적인 GC를 수행하기 위해 사용

 ### 1.5 가비지 컬렉터(Garbage Collector) 특징

- 일반적으로 CMS Collector가 Parallel Collector 보다 속도가 빠름

- Parallel Collector는 Full GC 마다 메모리 단편화 제거 작업을 수행하지만 CMS는 Concurrent mode failure 경고가 발생할 때만 메모리 단편화 제거 작업을 수행

- Stop The World : MinorGC 발생시 발생하며 모든 어플리케이션의 쓰레드가 중지하고 예외 X

- MinorGC : Young Generation 영역을 정리하는 것. 새로 생성된 객체는 Eden 영역에 위치한다. Eden 영역에서 GC가 한번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동된다. 이 과정을 반복해서 살아남는 객체는 일정시간 참조되고 있다는 뜻이므로 Old 영역으로 이동된다.

- MajorGC(Full GC) : Old Generation 영역을 정리하는 것. Old 영역에 있는 모든 객체들을 검사하여 참조되지 않는 객체들을 한꺼번에 삭제

## 2. 가비지 컬렉터

> 시스템에서 가비지 컬렉션을 수행하는 부분이 `가비지 컬렉터`

