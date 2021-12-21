---
title: Multiprocessing
excerpt: Multiprocessing, MultiThread

categories:
  - Python

tags:
  - Multiprocessing
  - MultiThread

toc: true
toc_sticky: true
toc_label: Multi
---

하하하하 ㅠㅠ 인생쓴맛 보고 공부하는 기본기본기본기..
평소에 더 노력할걸 ㅠ^ㅠ 
아무튼, 더 나은 사람이 되기 위해선 끝없이 공부해야함을 배우고 갑니다.. 🥲  

# 1. Process

- 운영체제에서 할당받는 자원 단위 (실행 프로그램)
- CPU 동작시간, 주소 공간 (독립적)
- Code, Data, Stack, Heap -> 독립적
- 최소 1개의 메인 스레드 보유
- 파이프, 파일, 소켓 등을 사용해서 프로세스간 통신 (Cost 높음) -> Context Switching

🔎️ Cost 높다 -> 통신 비용이 높다.
{: .notice--info}

# 2. Thread

- 프로세스 내에 실행 흐름 단위
- 프로세스 자원 사용
- Stack만 별도 할당 나머지(Code, Data, Heap)은 공유
- 메모리 공유(변수 공유)
- 한 스레드의 결과가 다른 스레드의 영향 끼침

# 3. Multi-Process

- 한 개의 단일 어플리케이션(응용프로그램) -> 여러 프로세스로 구성 후 작업 처리
- 한개 프로세스 문제 발생은 확산 없음 (프로세스 Kill)
- 캐시 체인지, Cost 비용 매우 높음(오버헤드), 복잡한 통신 방식 사용

# 4. Multi-Thread

- 한 개의 단일 어플리케이션(응용프로그램) -> 여러 스레드로 구성 후 작업 처리
- 시스템 자원 소모 감소(효율성), 처리량 증가(Cost 감소)
- 디버깅 어려움, 통신 부담 감소, 단일 프로세스에는 효과 미약, 자원 공유 문제(교착 상태), 프로세스 영향

