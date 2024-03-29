## 24.02.13 (화) 질문 내용 공유

1. **인덱스에 대해 설명해주세요**
2. **RDBMS 에서 Hashtable 이 아닌 B+Tree 를 사용하는 이유**
3. **클러스터드 인덱스와 넌클러스터드 인덱스 비교**
4. **인덱스를 사용했을 때 유리한 경우**
5. **리플리케이션과 클러스터링 비교**
6. **DB 튜닝이 무엇인지, 각 단계 설명**

---

관련 질문 정리

### ✅ **왜 보편적으로 레드 블랙 트리 대신 B-Tree 자료 구조를 DB 인덱스로 사용하는가?**

RedBlack-Tree는 무조건 하나의 노드에 하나의 데이터 요소만을 저장하므로 어떠한 요소를 탐색하든 참조 포인터 접근이 필수적이다. 반면, B-Tree는 하나의 노드에 여러 개의 데이터를 저장하므로 각 노드의 데이터 요소를 탐색할 때 참조 포인터 접근 없이 배열의 성질을 이용하여 빠르게 탐색이 가능하다. 결론적으로 참조 포인터의 접근 수가 B-Tree가 훨씬 적으므로 B-Tree를 인덱스의 자료 구조로 사용한다.

### ✅ **왜 보편적으로 배열 대신 B-Tree 자료 구조를 DB 인덱스로 사용하는가?**

배열은 데이터를 조회할 때만 B-Tree보다 빠르고, 나머지 데이터 저장, 수정, 삭제 시 배열이 B-Tree보다 월등히 느리므로 B-Tree를 인덱스의 자료 구조로 사용한다.

### ✅ **왜 보편적으로 해시 테이블 대신 B-Tree 자료 구조를 DB 인덱스로 사용하는가?**

해시 테이블 내의 데이터는 정렬이 되어 있지 않으므로 부등호 연산이 불가능하다. 인덱스의 특성상 기준 값보다 크거나 작은 요소를 탐색하는 경우가 많은데, 이러한 이유로 B-Tree를 인덱스의 자료 구조로 사용한다.

### ✅ **그러면 해시 테이블은 인덱스에서 사용되지 않는가?**

그렇지 않다. 해시 테이블은 등호 연산에는 특화되어 있으므로 해시 인덱스를 사용하는 경우도 있다. 보편적으로 잘 사용하지 않는다고 하면 맞다고 생각한다.

### ✅ 인덱스 사용하는 이유 무엇인가요 ?

**1. 인덱스를 사용하는 이유**

where 구문에 해당하는 열을 빨리 찾기 위해서

join 시 다른 테이블의 열을 빨리 추출하기 위해서

사용가능한 키의 최 좌측 접두사(leftmst prefix)를 가지고 정렬 및 그룹화를 하기 위해서

min() 또는 max(), count값을 찾기 위해

**2. 인덱스를 사용하지 않게 된다면**

서버의 Heap 영역에 데이터의 레코드들이 순서 없이 저장된다면, 특정 데이터를 찾기 위해선 **Full Scan(Table Scan) 방식**을 사용하게 된다. 이럴 경우 용량이 큰 테이블에서 처리 성능이 떨어질 것이다.

### ✅ 인덱스 장단점 무엇인가요 ?

**(1) 장점**

- 테이블 조회 속도 향상, 그에 따른 성능 향상
- 전반적 시스템 부하 줄임

**(2) 단점**

- 인덱스 관리 목적으로 DB의 약 10%되는 별도의 저장 공간 필요 (메모리 공간 차지)
- 인덱스 관리를 위한 추가 작업 필요
- 인덱스 잘못 사용 시 오히려 성능 저하되는 역효과

<aside>
💡 **RDBMS에서 인덱스 사용은 필수다. 일반적인 OLTB(온라인 트랜잭션 처리) 시스템의 경우 데이터 조회 업무가 90% 이상이기 떄문이다.**

</aside>

### ✅ **클러스터형 인덱스와 넌클러스터형 인덱스를 설명해주세요.**

- 쉽게 책에 비유하자면클러스터 인덱스는, 페이지를 알기 때문에 바로 그 페이지를 펴는 것이고,넌 클러스터 인덱스는, 뒤에 목차에서 찾고자 하는 내용의 페이지를 찾고 그 페이지로 이동하는 것과 같습니다. 테이블 스캔은 처음부터 한 장씩 넘기면서 내용을 찾는 것과 같습니다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/e2950218-da47-484d-ad70-1046d12a97ea/Untitled.png)

### ✅ 그렇다면 DBMS는 Index를 어떻게 관리하고 있나요?

B+Tree 인덱스 자료구조
자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이며,BTree 리프노드들을 LinkedList로 연결하여 순차 검색을 용이하게 합니다. 해시 테이블보다 나쁜 O(log2N)의 시간복잡도를 갖지만 일반적으로 사용되는 자료구조입니다

해시 테이블
컬럼의 값으로 생성된 해시를 기반으로 인덱스를 구현합니다.시간복잡도가 O(1)이라 검색이 매우 빠릅니다.부등호(<,>)와 같은 연속적인 데이터를 위한 순차 검색이 불가능하기 때문에 사용에 적합하지 않습니다.

### ✅ DB 튜닝(Tuning)이 무엇인지 그리고 튜닝의 3단계에 대해 설명해주세요.

DB 튜닝이란 DB의 구조나, DB 자체, 운영체제 등을 조정하여 DB 시스템의 전체적인 성능을 개선하는 작업

튜닝은 DB 설계 튜닝 → DBMS 튜닝 → SQL 튜닝 단계로 진행할 수 있다.

### **DB 튜닝 3단계 | (DB 설계 튜닝 → DBMS 튜닝 → SQL 튜닝)**

**1단계 : DB 설계 튜닝 (모델링 관점)**

- DB 설계 단계에서 성능 고려하여 설계
- 데이터 모델링, 인덱스 설계
- 데이터 파일, 테이블 스페이스 설계
- 데이터베이스 용량 산정

→ 튜닝 사례 : 반정규화, 분산파일 배치 

**2단계:  DBMS 튜닝 (환경 관점)**

- 성능을 고려하여 메모리나 블록 크기 지정
- CPU, 메모리 I/O에 관한 관점

→ 튜닝 사례 : Buffer 크기, Cache 크기

**3단계 : SQL 튜닝 (App 관점)**

- SQL 작성 시 성능 고려
- Join, Indexing, SQL Execution Plan

→ 튜닝 사례 : Hash/Join

---

### ✅ **인덱스는 보통 왜 사용하나요?**

인덱스는 데이터베이스의 성능 향상 수단으로 사용되는 가장 일반적인 방법입니다.

응답 시간이 늦은 SQL이 발견되면 우선 인덱스로 해결할 수 없는지를 검사하는 것이 튜닝의 제 1선택입니다.

인덱스의 장점으로는 SQL 문을 변경하지 않아도 성능을 개선할 수 있다는 점과 테이블의 데이터에 영향을 주지 않는다는 점이 있습니다.

### ✅ **보통 INDEX를 어느 컬럼에 걸어주나요? (⭐)**

보통 Cardinality(카니널러티)가 높은 열에 만듭니다.

Cardinality란 값의 분산도를 나타내는 단어로, 특정 열에 대해 많은 종류의 값을 가지고 있다면, Cardinality가 높다는 의미입니다.

그리고 크기가 큰 테이블에 만듭니다. 

제 경험으로 미루어 봤을 때 row 수가 약 80만 건 정도가 되면 인덱스가 없는 조회는 성능이 떨어졌습니다.

### ✅ **INDEX가 Hash가 아닌 B-tree를 사용하는 이유 (⭐⭐)**

SELECT 질의의 조건에는 부등호(<>) 연산도 포함이 됩니다.

동등 연산에 특화된 해쉬는 데이터베이스의 자료구조로 적합하지 않습니다.

### ✅ **다중 컬럼 인덱스가 안 걸리는 케이스 (⭐)**

복수의 키에 대해서 order by를 사용한 경우

연속하지 않은 컬럼에 대해 order by를 실행한 경우

desc와 asc를 혼합하여 사용한 경우

group by와 order by의 컬럼이 다른 경우

order by 절에 다른 표현을 사용한 경우

### ✅ **Replciation과 Clustering에 대해 설명해 주세요.**

**리플리케이션(Replciation)**

- 여러 개의 DB를 권한에 따라 수직적인 구조(Master-Slave)로 구축하는 방식입니다.
- 비동기 방식으로 노드들 간의 데이터를 동기화합니다.
- **장점** : 비동기 방식으로 데이터가 동기화되어 지연 시간이 거의 없습니다.
- **단점** : 노드들 간의 데이터가 동기화되지 않아 일관성있는 데이터를 얻지 못할 수 있습니다.

**클러스터링(Clustering)**

- 여러 개의 DB를 수평적인 구조로 구축하여 Fail Over한 시스템을 구축하는 방식입니다.
- 동기 방식으로 노드들 간의 데이터를 동기화합니다.
- **장점** : 1개의 노드가 죽어도 다른 노드가 살아 있어 시스템을 장애없이 운영할 수 있습니다.
- **단점** : 여러 노드들 간의 데이터를 동기화하는 시간이 필요하므로 리플리케이션에 비해 쓰기 성능이 떨어집니다.

---