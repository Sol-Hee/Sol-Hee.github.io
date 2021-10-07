---
title: Name Space, staticmethod
excerpt: class, instance 내의 네임 스페이스 & staticmethod

categories:
  - Python
tags:
  - class
  - instance
---

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

### staticmethod
- 정적 메소드
- class, instance 상관 없이 해당 메서드 호출 가능

테스트
```python
# class 생성
class test:    
    def not_static():
       print('Not static :)')
        
    @staticmethod
    def static():
       print('Hi !')
```
**not_static method를 인스턴스와 클래스기반으로 호출해보자**

*인스턴스 기반*
```python
test_instance = test()
print(test_instance.not_static())

'''
실행 결과
TypeError: not_static() takes 0 positional arguments but 1 was given
'''
```

*클래스 기반*
```python
print(test.not_static())

'''
실행 결과
Not static :)
'''
```

**static method를 인스턴스와 클래스 기반으로 호출해보자**

```python
# 인스턴스
test_instance = test()
print(test_instance.static())

# 클래스
print(test.static())
'''
실행결과
Hi !
Hi !
'''
```