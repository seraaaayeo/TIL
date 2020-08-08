## 파이썬 고급 문법
* dictionary = map
    - Map: key: value 자료구조 형태의 데이터.
    - JS object(JSON)이 이 형태의 데이터 포맷.
    - 다양한 언어에서 해당 자료구조 제공.
    - 따라서 파이썬에서도 Map 형태의 자료구조를 제공하기 위해 딕셔너리 등장.
    - 소켓통신, XML 이후에 등장. 값을 파싱하여 해석할 필요가 없이 simple하여 많이 쓰임.
    - json.org
* map() 
    - 기존에 있는 데이터 조작
    - map(function, iterable)
* filter()
    - 특정 조건 필터링
    - filter(function, iterable)
    - 리스트 중 function(특정 조건)에 맞는 data만 return
* lambda()
    * 가비지 컬렉션
        * 메모리 관리 기법
        * 프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게 된 영역(어떤 변수도 가리키지 않는 영역)을 해제하는 기능.
        * lambda: 익명함수이기 때문에 한 번 쓰이고 다음줄로 넘어가면 힙 메모리 영역에서 증발(가비지 컬렉터: 메모리 환원)
        * 장점 : 다음과 같은 버그를 줄이거나 막을 수 있다.
            - 유효하지 않은 포인터 접근 : 이미 해제된 메모리에 접근하는 버그.
            - 이중 해제 : 이미 해제된 메모리를 또다시 해제. 일부 메모리 할당 알고리즘에서 오류를 일으킬 수 있다.
            - 메모리 누수 : 더 이상 필요하지 않은 메모리가 해제되지 않고 남아있음. 메모리 누수가 반복되면 메모리 고갈로 프로긂이 중단될 수 있음.
        * 포인터 추적 방식 사용 : 한 개 이상의 변수가 접근 가능한 메모리는 앞으로 사용할 수 있는 메모리로 간주하고, 그 밖의 메모리를 해제하는 방식.
            - 접근 가능한 객체 : 어떤 변수가 직접, 간접적으로 가리키는 메모리.
            ```
            정의 1. 변수가 가리키는 객체. 변수는 콜 스택에서 정의된 지역 변수와 전역 변수를 모두 포함한다.
            정의 2. 접근 가능한 객ㅊ가 가리키는 모든 객체는 접근 가능하다.
            ```
* map: <map object at 0x034A6328>
    - object를 반환하므로 그 값이 궁금하면 list()를 사용하면 됨.
    - ex.list(map)

* Generator
    * interator와 같은 루프의 작용을 컨트롤하기 위해 쓰이는 특별한 함수 또는 루틴.
    * yield 구문을 이용해 한 번 호출할 때 마다 하나의 값만을 리턴.
        - 일반 반복자에 비해 아주 작은 메모리를 필요로 함.
    * 즉, generator는 iterator와 같은 역할을 한다.
    * 등장 이유: 한 번 일을 하고 사라지는 함수가 아닌, 하나의 일을 마치면 그 일을 기억하면서 대기하고 있다가 다시 호출되면 전의 일을 계속 이어서 하는 함수의 필요성 증가.
    * list 와 generator 성능 비교 : 백만명의 학생 정보가 들어가는 리스트 생성
        - list : 
        > 시작 전 메모리 사용량: 12.125MB
        > 종료 후 메모리 사용량: 13.65625MB
        > 총 소요된 시간: 1.375000 초
        - generator :
        > 시작 전 메모리 사용량: 12.17578125MB
        > 종료 후 메모리 사용량: 12.18359375MB
        > 총 소요된 시간: 0.000000 초


## 함수
* 문서화
    * Docstring: 코드에 포함된 문서. 함수, 클래스 모듈 등에 정의할 수 있다.
    * __doc__ : 작성한 문서를 확인 가능.

* 인자 호출 방식
    * call by value: 함수로 인자가 전달될 때 동일한 값을 가진 객체를 복사하여 전달.
    = val1이 전달된 것이 아니라 val1과 동이란 값을 가진 객체가 전달됨.
    * call by reference: 함수로 인자가 전달될 때 실제로 인자가 가진 참조 값을 전달.
    = 실제로 인자 객체를 그대로 전달.
    * 파이썬은 함수에 전달되는 인자의 타입에 의해 호출을 결정한다.
        * immutable 객체: int, float, str, tuples -> 값에 의한 호출
        * mutable 객체: list, set, dict -> 참조에 의한 호출

* 가변 인자 함수
    * 가변 인자 함수: 인자의 개수가 정해지지 않은 함수
    * *args 와 같이 *를 이용한 매개변수는 가변인자를 받을 수 있는 것으로 해석된다.
    * *를 사용하는 것을 packing한다고 표현하기도 한다.

* 가변 매개변수
    ```
    def print_n_times(n, *val):
        for i in range(n):
            print(val)
    
    print_n_times(3, "test") #("test",) ("test",) ("test",)
    ```

* 재귀함수
    - 재귀에서 주의할 것: 무한루프

* 로컬변수와 전역변수

* 일급함수(first class 함수)
    - 함수를 다른 변수와 동일하게 다루는 언어.
    - 함수를 다른 함수에 매개변수로 제공 가능.
    - 함수를 변수에 할당할 수 있음.

* 예외처리
    * try-except
        - try: 예외가 발생할 가능성이 있는 구문
        - except : 예외가 발생했을 때 실행할 구문
        - finally
        - else
    * Multi-exception handiling
        - as 키워드 사용.
        - Exception(부모타입), Value Error 등등(자식 타입)
        - 상속되는 예외를 처리할 때 자식타입 예외를 먼저 처리해야 함.

* Event 처리
    * 데코레이터

***

## 파이썬 기본문법
* string notation: 
    - single quotation(') - 1 character
    - double quotation(") - more than two character

* 튜플
    - 튜플을 이용한 변수 값 교환 가능!!!!
    ```
    a, b = 10, 20 #type: tuple
    a, b = b, a
    print(a, b) #20 10

* return tuples: 여러 개의 변수를 return할 때
    - return param1 -> 호출한 쪽에 하나의 데이터 전달
    - return param1, param2 -> (param1, param2) 튜플의 하나의 객체로 리턴됨.

* Thread: 최소 작업 단위

* format
    ```
    format_a = "{}만 원".format(5000)
    print(format_a)  #5000만 원

    format_b = "{} {}".format(1000, 5000)
    print(format_b)  #1000 5000

    format_c = "{:5f}".format(52.273)
    print(format_c)  #52.27300
    ```

* lower, upper, rstrip, isdigit, isalpha, find 등.


## 파이썬 모듈
* package = directory처럼 모듈이 모인 구조.
    - main.py는 엔트리 포인트로, test_package 폴더(디렉터리)는 패키지로 사용
* import = path 잡기
* sys 모듈
    - exit()의 경우에는 sys를 import하지 않아도 사용할 수 있음.
    ```
    sys.exit()
    exit()
    ```
* time: Unix time반환
    ```
    import time
    time.time()
    ```

* datetime
    ```
    import datetime
    
    today = datetime.datetime.now() #현재 시간 반환
    month = today.month #현재 월 반환
    date = today.day #현재 일 반환
    ```
    - datetime.datetime.now().hour
    - datetime.datetime.now().min
    - 현재 연, 월, 일, 시, 분, 초 반환 가능

***

## 객체지향
#### 모듈화
* 여러 모듈 중 실행할 모듈을 엔트리 포인트로 잡기.
    - ex.make_cal.py와 use_cal.py 모듈이 있을 때 use_cal.py를 엔트리 포인트로 잡는다.
    - make_cal.py 모듈은 엔트리 포인트에서 import한다.

#### Class
* __eq__와 같은 메소드는 여러 모듈에서 사용할 수 있다.
    - 최상위 class에서 정의되었기 때문.
* 클래스 참조 시점
    * 클래스 이름으로 참조할 경우
    * 인스턴스로 참조할 경우 : 객체취급. 참조할 때 마다 새로 초기화됨.