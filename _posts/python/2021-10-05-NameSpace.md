---
title: Name Space
excerpt: class, instance 내의 네임 스페이스

categories:
  - Python
tags:
  - class
  - instance
----
### Name Space
- 개체를 구분할 수 있는 범위

1. __dict__
   - 네임스페이스 확인
   
   | 📌 instance method를 class namespace에 저장 <br/> 함수 중첩해서 쓰는 경우 잘 없어 메모리 효율 높이려고 
   | - 인스턴스 네임 스페이스에 저장되면 인스턴스 생성할 때 마다 메모리 점유율 증가 
2. dir()
   - 네임스페이스 key 확인
3. __doc__
   - class 주석 확인
4. __class__
   - 어떤 class 로 만들어진 인스턴스인지 확인
