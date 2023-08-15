# 1.1 디자인 패턴

- 디자인 패턴 : 코드를 확장 가능하고 유지 및 관리하기 용이하게끔 구성하고자 하는 방법론
  - 코드를 유연하고 재사용 가능하게끔 유지

![img_1](https://github.com/dongsikchoi/CS-knowledge-python/assets/52738769/f67db36b-16f8-45e7-b147-b6693eff002b)

- 본서에는 따로 카테고리가 나뉘어있지 않으나 임의로 대분류에 맞게 순서 조정 진행

```
1. 생성 (Creational) 패턴
    1. 싱글톤(Singleton) 패턴
    2. 팩토리(Factory) 패턴
2. 행동 (Behavioral) 패턴
    1. 전략(Strategy) 패턴
    2. 옵저버(Observer) 패턴
    3. 이터레이터(Iteraitor) 패턴
3. 구조 (Structural) 패턴
    1. 프록시(Proxy) 패턴 & 프록시 서버
    2. 노출모듈(Revealing Module) 패턴
4. 아키텍쳐(Architecture) 패턴
    1. MVC 패턴 (Model-View-Controller)
    2. MVP 패턴 (Model-View-Presenter)
    3. MVVM 패턴 (Model-View-ViewModel)
```

## 싱글톤 패턴

![img_2](https://github.com/dongsikchoi/CS-knowledge-python/assets/52738769/26645bf2-3bb7-4f43-8676-d92d20b5ae2d)

- 하나의 클래스는 하나의 인스턴스만 가지는 패턴
  - A singleton class is a class that only allows creating one instance of itself.

### 샘플 코드

```python
class SingletonClass(object):
  def __new__(cls):
    if not hasattr(cls, 'instance'):
      cls.instance = super(SingletonClass, cls).__new__(cls)
    return cls.instance

singleton = SingletonClass()
new_singleton = SingletonClass()

print(singleton is new_singleton)

singleton.single_variable = "Singleton Variable"
print(new_singleton.single_variable)
```

### 싱글톤 패턴의 단점

- 전역 변수와 거의 같은 장단점을 가지고 있음
  - 편리하지만 코드의 모듈성을 해침
- 유닛 테스트 시 걸림돌 (**의존성 주입**; _DI_ _: Dependency Injection_)
  - 싱글톤에 의존적인 클래스를 다른 context에서 사용 시 해당 싱글톤도 같이 전달해야 하므로</br>

---

![img_3](https://github.com/dongsikchoi/CS-knowledge-python/assets/52738769/ab18ea6d-ec88-482d-90b2-2725ede9658d)

- Sample Code

  ```python
  class Email():
    # ...
    def send_message():
        # send msg code

  class EmailService():
    email = Email() # 의존성
    email.send_message()
  ```

- 의존성 주입의 장점
  - 코드의 재사용성, 유연성 ↑
  - 객체간 결합도가 낮아 한 클래스를 수정했을 때 다른 클래스도 함께 수정해야 하는 상황 X
  - 유지보수 및 테스트 용이
  - 확장성 ↑
- 의존성 주입의 단점

  - 책임이 분리되어 있으므로 절대적인 클래스 수가 늘어나 복잡성 ↑
  - 약간의 런타임 페널티 존재

- 의존성 주입 원칙
  - 상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야 함
