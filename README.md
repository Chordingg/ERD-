# ERD연습

<img width="406" alt="다운로드" src="https://github.com/Chordingg/ERD-/assets/157094467/432c68b4-5941-4a1c-9757-356e4287e682"> 
</br>
출처 : https://mangkyu.tistory.com/27

</br>
</br>

## ⭐ [온라인 전자상거래 플랫폼 개발 요구사항 분석]

온라인 전자상거래 플랫폼 개발 요구사항 분석 고객은 <br/>
고객코드, 고객명, 전화번호, 이메일 주소, 기본주소, 상세주소, 지역, 가입일로 되어있다. <br/>

고객은 지역별로 관리되도록 한다. <br/>

지역은 지역코드와 지역명으로 되어있고, 지역명은 대한민국의 지역코드 ('서울특별시') 02 를 이용한다. <br/>
한 지역에는 여러 고객이 있을 수 있다. <br/>

제품은 제품코드, 제품명, 가격으로 되어있다. <br/>

고객은 등록된 제품을 구매할 수 있다. <br/>
한 명의 고객은 여러 제품을 구매할 수 있고, 하나의 제품은 여러 고객이 구매할 수 있다. <br/>
고객이 제품을 구매 시 구매수량과 구매일자를 기록한다. <br/>

##### 👉 [객체 관계 정의서]

|객체명|속성명|||||||관계유형|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|고객|고객코드|고객명|전화번호|이메일|주소(기본주소,상세주소)|지역|가입일
|지역|지역코드|지역명|
|제품|제품코드|제품명|가격|
|----|----|----|----|----|----|----|----|----|
|구매|구매코드|구매수량|구매일자|||||M : N 
|관리|고객은 지역별로 관리|||||||1 : N 

![주석 2024-04-02 095800](https://github.com/Chordingg/ERD-/assets/157094467/18b28831-e655-4ded-a48a-dfb2e1a0d2aa)

![주석 2024-04-02 095914](https://github.com/Chordingg/ERD-/assets/157094467/c4372d4c-787a-4966-aebc-8b95ae0b2fbc)

![MySQL EER Diagram](https://github.com/Chordingg/ERD-/assets/157094467/598b4c49-0fb3-4e18-b2b8-152e161fcf0f)


***
</br>
</br>

## ⭐ [학사관리 시스템]

학생은 학번, 이름, 키, 학과코드로 이루어져 있습니다. <br/>
학과는 학과코드, 학과명으로 이루어져 있습니다.<br/>
교수는 교수코드, 교수명, 학과코드로 이루어져 있습니다.<br/>
개설과목은 과목코드, 과목명, 교수코드, 시작일, 종료일로 이루어져 있습니다.<br/>
수강은 학번, 과목코드로 이루어져 있습니다.<br/>

학과는 많은 학생을 가질 수 있고, 학생을 한 학과에 소속된다.<br/>
학과는 많은 교수를 가질 수 있고, 과목은 강의하는 교수 한 명이 지정된다.<br/>
과목은 수강하는 많은 학생을 가지고 학생은 많은 과목을 수강할 수 있다.<br/>

##### 👉 [객체 관계 정의서]

객체명 속성명<br/>
학생  (학생, 이름, 키)<br/>
학과  (학과코드, 학과명)<br/>
교수  (교수코드, 교수명)<br/>
과목  (과목코드, 과목명, 시작일, 종료일)<br/>

|객체명|속성명|||||
|:---|:---:|:---:|:---:|:---:|:---:|
|학생|학번|이름|키|학과코드||
|학과|학과코드|학과명|
|교수|교수코드|교수명|학과코드|
|개설과목|과목코드|과목명|교수코드|시작일|종료일|


|    |<center>참여객체/관계유형</center>|<center>속성</center>|
|----|---------------------:|:--------------------|
|소속|  학과  / 학생   |1 : N              
|    |  학과 / 교수   |1 : N            


|    |<center>참여객체/관계유형</center>|<center>속성</center>|
|----|---------------------:|:--------------------|
|강의|  교수 / 과목    |1 : N              
|수강|  학생 / 과목    |M : N   
