# 솔리디티 함수

- ***pure***
    - ***function*** 밖의 변수들을 읽지 못하고, 변경도 불가능
    
    ```solidity
    function read_a2() public pure returns(uint256) {
    uint256 b = 1;
    return 4+2+b;
    }
    ```
    
- ***view***
    - ***function*** 밖의 변수들을 읽을 수 있으나 변경 불가능
    
    ```solidity
    uint 256 public a = 1;
    
    function read_a() public view returns(uint256){
    return a+2;
    }
    ```
    
- ***pure* 와 *view* 둘다 명시하지 않을때**
    - ***function*** 밖의 변수들을 읽어서, 변경을 해야함
    
    ```solidity
    function read_a3() public view returns(uint256){
    a = 13;
    return a;
    }
    ```
    
- **솔리디티 예외처리**
    - 솔리디티에서는 3가지의 예외, 즉, exception을 처리하는 방법이 있습니다. 3가지 방법 모두 공통적으로 트랜잭션의 작업을 종료시키고, 현재까지 트랜잭션에 의해 변경되었던 블록체인상의 모든 상태를 원래의 초기상태로 복원을 시킵니다.
    - 예외를 처리하는 방법은 아래의 3가지 방법이 있습니다.
        - ***Assert***(***bool condition***)
            - 내부적인 상태 및 불변성(***invariant***) 검사 등에 적용
        - ***Require*** (***bool condition, string memory message***)
            - 입력 파라미터 또는 출력값 검사 등에 적용
            - ***message***는 ***optional***
        - ***Revert*** (***string memory reason***)
            - 예외를 즉시 발생시키고 상태를 복원(***reason***는 ***optional***)
- ***public / private / internal /* External**
    - ***public***
        
        솔리디티에서 함수는 기본적으로 **public**으로 선언된다. 즉, 누구나 (혹은 다른 컨트랙트) 컨트랙트의 함수를 호출하고 코드를 실행할 수 있다. 이는 컨트랙트를 공격에 취약하게 만들 수 있다. 그래서 ***기본적으로 함수를 private로 선언하고 공개할 만한 함수만 public으로 선언한다.***
        
    - ***private***
        
        private는 **컨트랙트 내의 다른 함수**들만이 이 함수를 호출하여 numbers 배열로 무언가를 추가할 수 있다는 것을 의미. (함수 인자명과 마찬가지로 private 함수명도 언더바(_)로 시작하는 것이 국룰)
        
    - ***internal***
        - internal은 함수가 정의된 컨트랙트를 상속하는 컨트랙트에서도 접근이 가능하다 점을 제외하면 private과 동일하다.
    - ***external***
        - external은 함수가 컨트랙트 바깥에서만 호출될 수 있고 컨트랙트 내의 다른 함수에 의해 호출될 수 없다는 점을 제외하면 public과 동일.
- ***mapping***
    - ***mapping***은 ***KeyType*** => ***ValueType***의 문법구조를 가진다.
    - ***keyType***은 모든 기본값(***integer***등), ***bytes***, ***string***, 컨트랙트가 될 수 있다.
    - ***valueType***은 다른 맵핑이나 배열을 포함한 모든 유형이 될수 있다.
    - 맵핑은 반복할 수 없다.
