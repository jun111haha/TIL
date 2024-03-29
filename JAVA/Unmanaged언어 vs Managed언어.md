# Managed Language?
자바를 공부하면서 자바는 대표적인 Managed Language 라는 말을 간간히 보았다.

Managed Language에 대한 정확한 정의는 Wikipedia에의 하면 MS사(혹은 MS진영)에서 C#을 Managed Code라 칭한데서 비롯된거 같다.

즉, C#이 Common Language Runtime(자바의 JVM같은) 위에서 작동되므로, 이런 모습이 Managed 되고있는 언어라는거다.

이후 Managed Code라는 용어가 확장되어

특정 런타임 환경 내에서 관리되고 있는 언어를 통칭해 Managed Language라 부르고있다.

자바의 경우 대표적인 Managed Languge로 분류되는데

자바의 프로그램 코드는 하드웨어 -> OS -> JVM -> JAVA APP 의 과정으로 JVM위에서 컴파일 되며, 실행파일 또한 JVM 위에서 동작한다.

이때 JVM은 JAVA APP의 메모리관리(Garbage Collector)를 비롯해서 파일 시스템 엑세스, 네트워크 입출력을 위한 리소스관리 등 다양한 관리역할을 수행한다.

자바와 같이 특정 런타임 환경 내에서 관리되는 언어들로는 파이썬, 자바스크립트, C#등이 있다.

장단점?
사용자가 놓치기 쉬운 영역들을 관리해주므로 코딩이 빠르고 간편하며, Memory Leak의 위험에서 상대적으로 안전하다.

하지만 코드가 실행시에 해석(Interpret) 되는 과정을 거치므로 속도가 느리며 GC로 인한 예기치못한 상황에 맞닥뜨릴수 있다.

# Unmanged Language?
위의 논리를 따라 특정 런타임 환경의 관리를 받지 않는 모든 언어는 Unmanaged Language라고 정의할 수 있다.

C/C++과 같은 언어가 대표적인 Unmanaged Languaged 이다.

여기서 주의할 점은 Managed와 Unmanaged를 구분하는 기준이 메모리의 자동관리 가 아니라는 점이다.

Rust가 메모리의 자동관리를 하는 Unmanged Language의 대표적 사례라고 할 수 있다.

장단점
Unmanaged Language에 비해 상대적으로 빠르며, 메모리의 할당과 해제를 사용자의 의도에 따라 세밀하게 조정할수 있으므로, 프로그래밍 자유도가 높고 최적화가 용이하다.

하지만 프로그래머가 실수할 경우 Memory Leak이 발생할 수 있다.

레퍼런스.  
https://en.wikipedia.org/wiki/Managed_code.  
https://algorfati.tistory.com/m/113   
https://blog.seulgi.kim/2019/04/managed-language-vs-unmanaged-langauge.html
