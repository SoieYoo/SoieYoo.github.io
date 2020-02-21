### 컬렉션 프레임워크란?
   *  자바에서 컬렉션 프레임워크(collection framework)란 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미합니다.

   *  즉, 데이터를 저장하는 자료 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것입니다.

   *  이러한 컬렉션 프레임워크는 자바의 인터페이스(interface)를 사용하여 구현됩니다.

### 컬렉션 프레임워크 주요 인터페이스

   *  List 인터페이스 **List<<E>>**
      *  순서가 있는 데이터의 집합으로, 데이터의 중복을 허용합니다.
   *  Set 인터페이스 **Set<<E>>**
      *  순서가 없는 데이터의 집합으로, 데이터의 중복을 허용하지 않습니다.
   *  Map 인터페이스 **Map<K,V>**
      *  키와 값의 한 쌍으로 이루어지는 데이터의 집합으로, 순서가 없습니다.
      *  이때 키는 중복을 허용하지 않지만, 값은 중복될 수 있습니다.

### 구현 클래스
   *  List 인터페이스
      *  Vector, ArrayList, LinkedList, Stack, Queue
   *  Set 인터페이스
      *  HashSet, TreeSet
   *  Map 인터페이스
      *  HashMap, TreeMap, Hashtable, Properties

### 구현 클래스 예제
   * **List 인터페이스 중 ArrayList 메소드**

``` java
ArrayList<Integer> arrList = new ArrayList<Integer>();
```

   *  **List 인터페이스 중 LinkedList<E>클래스**
``` java
LinkedList<String> lnkList = new LinkedList<String>();

//ArrayList와 LinkedList의 차이는 사용 방법이 아닌, 내부적으로 요소를 저장하는 방법에 있습니다.
```

   *  **List 인터페이스 중 Stack<> 클래스**
      *  스택 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 후입선출(LIFO)의 시멘틱을 따르는 자료 구조입니다.
      *  즉, 가장 나중에 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조입니다.
      *  더욱 복잡하고 빠른 스택을 구현하고 싶다면 Deque 인터페이스를 구현한 ArrayDeque 클래스를 사용하면 됩니다.

```java

Stack<Integer> st = new Stack<Integer>(); // 스택의 생성

Deque<Integer> st = new ArrayDeque<Integer>();


//ArrayDeque 클래스는 Stack 클래스와는 달리 search() 메소드는 지원하지 않습니다.
```

   *  **Queue<<E>> 인터페이스**
      *  Queue 인터페이스를 직간접적으로 구현한 클래스는 상당히 많습니다.
      *  그중에서도 Deque 인터페이스를 구현한 LinkedList 클래스가 큐 메모리 구조를 구현하는 데 가장 많이 사용됩니다.
      *  큐 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 선입선출(FIFO)의 시멘틱을 따르는 자료 구조입니다.
      *  즉, 가장 먼저 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조입니다.
      *  더욱 복잡하고 빠른 큐를 구현하고 싶다면 Deque 인터페이스를 구현한 ArrayDeque 클래스를 사용하면 됩니다.

```java

LinkedList<String> qu = new LinkedList<String>(); // 큐의 생성

Deque<String> qu = new ArrayDeque<String>();

//Java SE 6부터 지원되는 ArrayDeque 클래스는 스택과 큐 메모리 구조를 모두 구현하는데 가장 적합한 클래스입니다.
```

   *  **Set 컬렉션 클래스 중 HashSet<>클래스**
      *  HashSet 클래스는 Set 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나입니다.
      *  JDK 1.2부터 제공된 HashSet 클래스는 해시 알고리즘(hash algorithm)을 사용하여 검색 속도가 매우 빠릅니다.
      *  이러한 HashSet 클래스는 내부적으로 HashMap 인스턴스를 이용하여 요소를 저장합니다.
      *  HashSet 클래스는 Set 인터페이스를 구현하므로, 요소를 순서에 상관없이 저장하고 중복된 값은 저장하지 않습니다.
      *  만약 요소의 저장 순서를 유지해야 한다면 JDK 1.4부터 제공하는 LinkedHashSet 클래스를 사용하면 됩니다.


```java
HashSet<String> hs01 = new HashSet<String>();
 ```
   *  
      *  Collection 인터페이스에서는 Iterator 인터페이스를 구현한 클래스의 인스턴스를 반환하는 iterator() 메소드를 정의하여 각 요소에 접근하도록 하고 있습니다.
      *  요소의 저장 순서를 바꿔도 저장되는 순서에는 영향을 미치지 않는 것을 확인할 수 있습니다.
      *  또한, add() 메소드를 사용하여 해당 HashSet에 이미 존재하는 요소를 추가하려고 하면, 해당 요소를 저장하지 않고 false를 반환하는 것을 볼 수 있습니다.
      *  이때 해당 HashSet에 이미 존재하는 요소인지를 파악하기 위해서는 내부적으로 다음과 같은 과정을 거치게 됩니다.
      *   1. 해당 요소에서 hashCode() 메소드를 호출하여 반환된 해시값으로 검색할 범위를 결정합니다.
      *  2. 해당 범위 내의 요소들을 equals() 메소드로 비교합니다.
      *  따라서 HashSet에서 add() 메소드를 사용하여 중복 없이 새로운 요소를 추가하기 위해서는 hashCode()와 equals() 메소드를 상황에 맞게 오버라이딩해야 합니다.


   *  **Set 컬렉션 클래스 중 TreeSet<>클래스**
      *  TreeSet 클래스는 데이터가 정렬된 상태로 저장되는 이진 검색 트리(binary search tree)의 형태로 요소를 저장합니다.
      *  이진 검색 트리는 데이터를 추가하거나 제거하는 등의 기본 동작 시간이 매우 빠릅니다.
      *  JDK 1.2부터 제공되는 TreeSet 클래스는 NavigableSet 인터페이스를 기존의 이진 검색 트리의 성능을 향상시킨 레드-블랙 트리(Red-Black tree)로 구현합니다.
      *  TreeSet 클래스는 Set 인터페이스를 구현하므로, 요소를 순서에 상관없이 저장하고 중복된 값은 저장하지 않습니다.

```java
TreeSet<Integer> ts = new TreeSet<Integer>();
```

   *  **Map 컬렉션 클래스**
      *  Map 인터페이스는 Collection 인터페이스와는 다른 저장 방식을 가집니다.
      *  Map 인터페이스를 구현한 Map 컬렉션 클래스들은 키와 값을 하나의 쌍으로 저장하는 방식(key-value 방식)을 사용합니다.
      *  여기서 키(key)란 실질적인 값(value)을 찾기 위한 이름의 역할을 합니다.
      *  요소의 저장 순서를 유지하지 않습니다.
      *  키는 중복을 허용하지 않지만, 값의 중복은 허용합니다. 
      *  대표적인 Map 컬렉션 클래스에 속하는 클래스는 HashMap<K,V> , HashTable<K,V>, TreeMap<K,V>가 있습니다.


   *   **Map 클래스 중 HashMap 클래스**
      *  JDK 1.2부터 제공된 HashMap 클래스는 해시 알고리즘(hash algorithm)을 사용하여 검색 속도가 매우 빠릅니다.
      *  HashMap 클래스는 Map 인터페이스를 구현하므로, 중복된 키로는 값을 저장할 수 없습니다.
      *  하지만 같은 값을 다른 키로 저장하는 것은 가능합니다.

```java
HashMap<String, Integer> hm = new HashMap<String, Integer>();

//keySet() 메소드는 해당 맵에 포함된 모든 키 값들을 하나의 집합(Set)으로 반환해 줍니다.
// 향상된 for문은 배열과 컬렉션 프레임워크에서 해당 인스턴스에 저장된 모든 요소를 순회해야할 경우에 자주 사용됩니다.
```

   *  **HashTable 클래스**
      *   현재에는 기존 코드와의 호환성을 위해서만 남아있으므로, Hashtable 클래스보다는 HashMap 클래스를 사용하는 것이 좋습니다.

   *  **TreeMap<K,V>클래스**
      *  TreeMap 클래스는 키와 값을 한 쌍으로 하는 데이터를 이진 검색 트리(binary search tree)의 형태로 저장합니다.
      *  이진 검색 트리는 데이터를 추가하거나 제거하는 등의 기본 동작 시간이 매우 빠릅니다.
      *  JDK 1.2부터 제공된 TreeMap 클래스는 NavigableMap 인터페이스를 기존의 이진 검색 트리의 성능을 향상시킨 레드-블랙 트리(Red-Black tree)로 구현합니다.
      *  TreeMap 클래스는 Map 인터페이스를 구현하므로, 중복된 키로는 값을 저장할 수 없습니다.
      *  하지만 같은 값을 다른 키로 저장하는 것은 가능합니다.

```java
TreeMap<Integer, String> tm = new TreeMap<Integer, String>();
```
