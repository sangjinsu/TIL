# Go 언어 가비지 컬렉터

가비지 컬렉터는 불필요한 메모리를 청해서 재사용하도록 한다

문제점은 필요 없어진 인스턴스를 찾고 메모리를 정리하는 데 CPU를 사용해 성능 저하, 프로그램 멈춤, 사용 메모리 상승 등이 있다.

### 가비지 컬렉터 알고리즘

#### mark and sweep

모든 메모리 블록을 검사하고 사용하고 있으면 1 아니면 0으로 표시한 뒤 0으로 표시된 모든 메모리 블록을 삭제한다. 완전 검색이 필요하므로 CPU 성능이 많이 필요하고 검사 도중 메모리 변경이 되어서는 안되기 때문에 프로그램을 멈춰야 합니다

#### tri-color mark and sweep

0, 1, 2 로 메모리 블록을 표시합니다.

검사하지 않은 메모리 - 회색

사용하지 않는 메모리 - 흰색

이미 검사가 끝난 메모리 - 검은색

회색 블록을 검은색으로 바꾼 뒤 바뀐 검은색 블록을 참조 중인 모든 블록을 회색으로 바꿉니다. 

모든 회색 블록이 없어질 때까지 이 작업을 반복합니다

단점으로는 메모리 블록을 완전 검색하므로 속도가 느리고 메모리 상태가 계속 변경되어 메모리를 어느 시점에 삭제할지 결정하기 힘듭니다. 속도가 느려 메모리 삭제 속도보다 할당 속도가 더 빠르면 메모리가 지속적으로 증가하여 프로그램을 완전 멈추고 완전 탐색해야 합니다

#### moving object

삭제할 메모리를 마킹하고 한쪽으로 압축하여 한꺼번에 삭제하는 방식입니다

메모리를 압축하고 삭제하기 때문에 메모리 [단편화](https://ko.wikipedia.org/wiki/%EB%8B%A8%ED%8E%B8%ED%99%94)가 생기지 않습니다

단점으로는 메모리 위치 이동이 쉽지 않다는 점이다. 개체들은 연관 관계를 가지므로 메모리 블록 이동시 모든 연관 블록에 대한 조작 행위를 멈춰야 한다. 이 과정에서 CPU 성능을 많이 소비하고 프로그래밍 언어 레벨에서 메모리 이동이 쉬운 구조를 가지고 있어야 한다 

#### generational garbage collection

최근에 할당된 메모리 블록부터 먼저 검사하는 방식이다.

최근에 할당된 메모리 블록 순서대로 1세대, 2세대, 3세대, 4세대로 나뉘며 차례대로 불필요한 메모리를 삭제한다.

단점으로는 구현이 복잡하고 메모리 블록을 세대별로 이동해야 하는 문제가 있다

### Go 언어 가비지 컬렉터

- 동시성 삼색 표시 수집
- concurrent tri-color mark and sweep garbage collection

멈춤 시간을 매우 짧게 유지하면서 가비지 컬렉팅을 합니다. generational garbage collection을 사용하지 않습니다. 메모리 이동 비용이 들지 않고 매우 짧은 프로그램 멈춤만 필요합니다.

단점으로는 추가 힙 메모리가 필요하고 실행 성능이 저하될 수 있습니다. 메모리 할당 속도가 삭제 속도보다 빠르면 프로그램을 멈추고 완점 검색을 해야 합니다. 그래서 메모리 할당을 자주 하는 것이 좋지 않습니다.



### 쓰레기 줄이는 방법

#### 1. 불필요한 메모리 할당 없애기

##### 슬라이스 크기 증가

슬라이스가 append()에 의해 크기가 증가될 때 2배 크기의 배열을 할당합니다. 그러므로 불필요한 메모리 할당을 줄이기 위해 요소 개수가 예상되는 슬라이스를 만들 때는 예상 개수만큼 초기에 할당해 사용합니다

##### string 합산

문자열은 불변이기 때문에 문자열 조작은 항상 새로운 메모리 할당을 유발한다. `string.Builder` 를 사용하는게 좋다



