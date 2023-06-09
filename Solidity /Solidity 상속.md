# 상속 (Class Inheritance)

- **특징**
    - 기존에 정의해둔 클래스의 기능을 그대로 물려받을 수 있다.
    - 기존 클래스에 기능 일부를 추가하거나, 변경하여 새로운 클래스를 정의한다.
    - 코드를 재사용할 수 있게된다.
    - 상속 받고자 하는 대상인 기존 클래스는 (***Parent, Super, Base class*** 라고 부른다.)
    - 상속 받는 새로운 클래스는(***Child, Sub, Derived class*** 라고 부른다.)
    - 의미적으로 is-a관계를 갖는다
    - 물려주는 클래스를 부모클래스(***Super class***), 물려받는 클래스를 자식클래스(***Sub class***)
- ***super***
    
    override가 되지 않음
    
    ```solidity
    #########################################
    ### super의  다른 사용 예
    ### 부모클래스에도 init, prn 
    ### 자식클래스에도 init, prn 이 둘다 있을때 
    ### 이렇게 부모와 자식에 같은 def 이름이 있는 중복 def를 오버라이딩이라 함
    ### 오버라이딩은 [6]번에서 다시봄- 여기서는 init나 prn처럼 같은 함수가 있어도 부모함수를 호출하지 않으면
    ### 자식함수(메서드)가 실행되어서 부모의 함수(메서드)를 다룰때는 super 또는 부모함수().메서드() 로 실행됨을 알고 있으면 됨
    ##########################################
    class 부모():
        def __init__(self):
            self.값=30
            print('부모클래스 프린트임')
            
        def prn(self):
            print('★'*10)
            
    class 자식(부모):
        def __init__(self):
            print('자식클래스 프린트임')
            
        def prn(self):
            print('-'*10)
    출력=자식()
    출력.prn()                         # 자식클래스에 있는 __init__가 먼저 실행됨
    super(자식, 출력).__init__()       #자식클래스의 부모값을 실행함
    super(자식, 출력).prn()            # 자식클래스의 부모값을 실행함
    
    /*
    출력ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ 
    자식클래스 프린트임
    ----------
    부모클래스 프린트임
    ★★★★★★★★★★
    */
    ```
    
- ***override***
    - override된 함수는 상위 컨트랙트의 함수를 대체하게 되며, 하위 컨트랙트의 객체에서 호출되면 override된 함수가 호출된다
    - 부모 클래스의 method를 재정의(override)
    - 하위 클래스(자식 클래스) 의 인스턴스로 호출시, 재정의된 메서드가 호출됨
    - 아래코드 출처 및 설명
        - 메서드 오버라이딩(Method Overriding)이란, 여러 클래스에 걸쳐서 같은 이름의 메서드를 만드는 것이다. 예를 들어 부모 클래스, 전사 캐릭터 클래스, 마법사 캐릭터 클래스에 공통으로 attack이라는 메서드가 있지만, 각각 하는 일이 다를 때는 다음처럼 같은 이름의 메서드를 클래스별로 구현하면 된다. 이렇게 되면 부모 클래스에서 만든 메서드 정의를 자식 클래스에서는 변경해서 사용한다.
        
        ```solidity
        class Character(object):
            def __init__(self):
                self.life = 1000
                self.strength = 10
                self.intelligence = 10
        
            def attacked(self):
                self.life -= 10
                print("공격받음! 생명력 =", self.life)
        
            def attack(self):                              ####  ---> 부모클래스의 attack
                print("공격!")
                
        class Warrior(Character):
            def __init__(self):
                super(Warrior, self).__init__()
                self.strength = 15
                self.intelligence = 5
        
            def attack(self):                               ####  ---> 자식클래스의 attack
                print("육탄 공격!")
        
                
        class Wizard(Character):
            def __init__(self):
                super(Wizard, self).__init__()
                self.strength = 5
                self.intelligence = 15
        
            def attack(self):                          ####  ---> 자식클래스의 attack
                print("마법 공격!")
                
        a = Character()    #부모클래스 인스턴스 생성
        a.attack()     #==> 부모클래스의 attack 메서드 실행
            
        b = Warrior()      #자식클래스 인스턴스 생성
        b.attack()    ##--> 자식클래스의 attack 메서드 실행  (21번 행 실행됨)
        
        c=Wizard(); c.attack() # --31번 행 실행됨
        super(Wizard,c).attack()  # 부모 attack 실행
        ```
