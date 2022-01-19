## Java Collections Framework

![jvm](https://user-images.githubusercontent.com/60098769/150152629-2b2ea86d-855b-47ce-a4a7-c8c6835e7f6a.png)

- Map
    - 검색할 수 있는 인터페이스
    - 데이터를 삽입할 때 Key와 Value의 형태로 삽입되며, Key를 이용해서 Value를 얻을 수 있다.
- Collection
    - List
        - 순서가 있는 Collection
        - 데이터를 중복해서 포함할 수 있다.
    - Set
        - 집합적인 개념의 Collection
        - 순서의 의미가 없다.
        - 데이터를 중복해서 포함할 수 없다.

- Collections Framework 선택 과정
    - Map과 Collection 인터페이스 중 선택  
      1-1. Collection 선택 시 사용 목적에 따라 List와 Set중 선택
    - 사용 목적에 따라 Map, List, Set 각각의 하위 구현체를 선택  
      2-1. Map: HashMap, LinkedHashMap, HashTable, TreeMap  
      2-2. List: LinkedList, ArrayList  
      2-3. Set: TreeSet, HashSet  


### java Map 인터페이스 구현체의 종류 
- HashMap
    - Entry<K,V>의 배열로 저장되며, 배열의 index는 내부 해쉬 함수를 통해 계산된다.
    - 내부 hash값에 따라서 키순서가 정해지므로 특정 규칙없이 출력된다.
    - key와 value에 null값을 허용한다.
    - 비동기 처리
    - 시간복잡도: O(1)
- LinkedHashMap
    - HaspMap을 상속받으며, Linked List로 저장된다.
    - 입력 순서대로 출력된다.
    - 비동기 처리
    - 시간복잡도: O(n)
- TreeMap
    - 내부적으로 레드-블랙 트리(Red-Black tree)로 저장된다.
    - 키값이 기본적으로 오름차순 정렬되어 출력된다.
    - 키값에 대한 Compartor 구현으로 정렬 방법을 지정할 수 있다.
    - 시간복잡도: O(logn)
- ConCurrentHashMap
    - multiple lock
    - update할 때만 동기 처리
    - key와 value에 null값을 허용하지 않는다.
- HashTable
    - single lock
    - 모든 메서드에 대해 동기 처리
    - key와 value에 null값을 허용하지 않는다.


### java Set 인터페이스 구현체의 종류
- HashSet
    - 저장 순서를 유지하지 않는 데이터의 집합이다.
    - 해시 알고리즘(hash algorithm)을 사용하여 검색 속도가 매우 빠르다.
    - 내부적으로 HashMap 인스턴스를 이용하여 요소를 저장한다.
- LinkedHashSet
    - 저장 순서를 유지하는 HashSet
- TreeSet
    - 데이터가 정렬된 상태로 저장되는 이진 탐색 트리(binary search tree)의 형태로 요소를 저장한다.
    - 이진 탐색 트리 중에 성능을 향상시킨 레드-블랙 트리(Red-Black tree)로 구현되어 있다.
    - Compartor 구현으로 정렬 방법을 지정할 수 있다.


### java List 인터페이스 구현체의 종류
- ArrayList
    - 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 데이터 검색에 적합하다.
    - 데이터의 삽입, 삭제 시 해당 데이터 이후 모든 데이터가 복사되므로 삽입, 삭제가 빈번한 데이터에는 부적합하다.
- LinkedList
    - 양방향 포인터 구조로 데이터의 삽입, 삭제 시 해당 노드의 주소지만 바꾸면 되므로 삽입, 삭제가 빈번한 데이터에 적합하다.
    - 데이터의 검색 시 처음부터 노드를 순회하므로 검색에는 부적합하다.
    - 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰인다.
- Vector
    - 내부에서 자동으로 동기화 처리가 일어난다.
    - 성능이 좋지 않고 무거워 잘 쓰이지 않는다.

https://gmlwjd9405.github.io/2017/10/01/basic-concepts-of-development-java.html
