## mybatis에서  리턴타입 int와 _int 차이

org.apache.ibatis.type.TypeAliasRegistry 를 확인해보았습니다.

```java
public class TypeAliasRegistry {

  public TypeAliasRegistry() {

    registerAlias("int", Integer.class);
    registerAlias("integer", Integer.class);

    registerAlias("_int", int.class);
    registerAlias("_integer", int.class);
  }
}
```

   *  resultType="int" 와 resultType="integer" 는 Integer.class 입니다. wrapper 클래스로 객체 자체입니다. 
   *  resultType="_int" 와 resultType="_integer" 는 int.class 입니다. 간단한 산술 연산을 위한 자료형입니다. 
   *  Integer.class 객체는 int값을 저장할 수 있습니다.
   *  (ex)ArrayList<(Integer)>는 허용하지만 ArrayList<(int)>는 허용하지 않습니다.
   *  Integer는 클래스로 null을 return할 수 있지만, int 타입은 런타임오류를 발생시킵니다.
