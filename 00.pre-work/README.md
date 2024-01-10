<img src="https://companieslogo.com/img/orig/MDB_BIG-ad812c6c.png?t=1648915248" width="50%" title="Github_Logo"/> <br>


# MongoDB Atlas Training for LGU Plus

### Preparing for Hands-on


#### Atlas login

상단의 Atlas에서 "RFC FIELD MARKETING1"을 클릭 하면 권한이 부여된 Project를 볼 수 있습니다. 이를 클릭 합니다.

<img src="/00.pre-work/images/images13.png" width="90%" height="90%">   

Project에 성공적으로 접근 하면 현재 사용 중인 IP에 대한 접근 허용 여부에 대한 메시지를 볼 수 있습니다. Add current IP를 클릭 하여 현재 사용중인 IP 주소로 접근을 허용 하여 줍니다.

<img src="/00.pre-work/images/images14.png" width="90%" height="90%">   


#### Database Account 생성
Atlas 데이터베이스 클러스터를 접근하기 위한 계정 생성으로 Security 메뉴에 Database Access를 클릭 하여 계정을 생성 할 수 있습니다.    
Hands-on에서는 Id/password를 이용하는 방식의 데이터베이스 계정을 생성 합니다.   
<img src="/00.pre-work/images/images08.png" width="90%" height="90%">  
계정은 atlas-account로 하여 생성 합니다. Built-in Role 은 편의상 Read and Write to any database 를 선택합니다.

#### 초기 데이터 로드
생성된 데이터 베이스 클러스터에 초기 샘플 데이터를 적재하여 Hands on을 진행 합니다.   
Database 메뉴를 클릭 하면 생성된 데이터 베이스 클러스터를 볼 수 있습니다. 최초에는 데이터가 없음으로 클러스터 메뉴 버튼을 "..."을 클릭 하면 추가 메뉴 중 Load Sample Dataset 을 선택 합니다.   
생성이 완료된 후 Browse Collections를 클릭하먄 데이터를 볼 수 있습니다.
생성된 데이터 베이스는 sample_airbnb외 8개의 데이터베이스가 생성 되고 최소 1개 이상의 컬렉션(테이블)이 생성되게 됩니다.
<img src="/00.pre-work/images/images15.png" width="90%" height="90%"> 


#### 기타 필요한 소프트웨어
MongoDB에 접속하고 데이터를 조회 하는 GUI Tool (Compass)를 다운로드 합니다.

Compass :   
https://www.mongodb.com/products/compass

Mongosh :
https://www.mongodb.com/docs/mongodb-shell/install/

