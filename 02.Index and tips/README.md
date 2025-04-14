<img src="https://companieslogo.com/img/orig/MDB_BIG-ad812c6c.png?t=1648915248" width="50%" title="Github_Logo"/> <br>


# MongoDB Atlas Training for LGU Plus

## Index and Tips
생성한 컬렉션에 인덱스를 생성하여 빠른 데이터 엑세스가 되는 것을 확인 합니다.

### [&rarr; Index on Movies](#Index)

<br>


### Index

sample_mflix.movies 에서 2000년 이후에 개봉된 영화 중 "Bill Murray"가 출연한 영화 리스트를 검색 하고 제목 순서로 출력 합니다.   

Compass에서 movies 컬렉션을 선택 하고 Explain Plan 에서 실행 합니다.   
````
db.movies.find(
	{
    	"cast":"Bill Murray",
    	"year":{$gte:2000}
	}
).sort(
	{"title":1}
)
````
<img src="/02.Index and tips/images/image01.png" width="100%" height="100%">     

No index available for this query 로 인덱스가 사용 되지 않은 것을 확인 할 수 있으며 Dcouments Examined의 갯수가 23530으로 전체 문서가 스캔 된 것을 확인 할 수 있습니다.    
또한 Documnets Returned 가 12인 것으로 전체 문서 중 12개 문서가 리턴된 것으로 12개 문서를 찾기 위해 23530 문서를 검색한 것으로 비효율적인 것을 알 수 있습니다.

E-S-R 규칙에 맞추어 인덱스를 생성 하고 Explain에서 개선된 사항을 확인 합니다.


#### Index 생성

테스트를 위해 cast - year - title 순서로 인덱스를 생성 하고 테스트 합니다.   

<img src="/02.Index and tips/images/image02.png" width="50%" height="50%">     


동일한 쿼리를 수행 하여 봅니다.    

<img src="/02.Index and tips/images/image03.png" width="90%" height="90%">     

문서 스캔이 Index 스캔으로 변경 되고 기존에 비해 성능이 개선된 것을 확인 합니다.  

첫 번째에서 IXSCAN으로 생성한 인덱스를 이용하여 12개의 문서가 검색된 것을 확인 할 수 있습니다. 이후 정렬 과정을 거친 후 데이터가 반환 되는 것을 확인 할 수 있습니다. 

인덱스를 ESR 순서로 작성합니다. (cast-title-year)   
동일한 쿼리를 실행 하여 플랜을 확인 합니다.    

<img src="/02.Index and tips/images/image04.png" width="90%" height="90%">     

#### Covered Query

다음 인덱스(type, year)를 생성 하고 Query에 대한 Explain을 확인 합니다.   

<img src="/02.Index and tips/images/image40.png" width="40%" height="40%"> 

인덱스 생성 이후 다음 내용을 Query를 작성하고 Explain을 확인 합니다.   

````
db.movies.find(
	{"type" : "movie", "year" : {$gte:2000}}
).explain("executionStats")
````

Comapss를 이용한 Explain은 다음과 같습니다.   

<img src="/02.Index and tips/images/image41.png" width="70%" height="70%"> 

12440건의 데이터를 검색하였으며 Fetch 시간이 16ms가 소요 된 것을 확인 할 수 있습니다.  

Query를 변경하여 Projection을 추가 하여 주고 테스트를 진행 합니다. (type, year 만 출력 하도록 합니다.)   

````
db.movies.find(
	{"type" : "movie", "year" : {$gte:2000}}, {type:1, year: 1, _id:0}
).explain("executionStats")
````

Compass에 해당 Query 조건을 입력 하고 Explain을 클릭 합니다.   

<img src="/02.Index and tips/images/image42.png" width="70%" height="70%"> 

결과를 확인해 보면 Index에서 Projection 항목을 가져올 수 있어 디스크에서 데이터를 읽어 들이는 Fetch 과정이 생략된 것을 볼 수 있습니다. 이로 인해 총 소요 시간이 매우 단출 된 것을 확인 할 수 있습니다.

<img src="/02.Index and tips/images/image43.png" width="70%" height="70%"> 
