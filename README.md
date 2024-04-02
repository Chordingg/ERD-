# ERD연습
[온라인 전자상거래 플랫폼 개발 요구사항 분석]

<img width="406" alt="다운로드" src="https://github.com/Chordingg/ERD-/assets/157094467/432c68b4-5941-4a1c-9757-356e4287e682">

![주석 2024-04-02 095800](https://github.com/Chordingg/ERD-/assets/157094467/18b28831-e655-4ded-a48a-dfb2e1a0d2aa)

![MySQL EER Diagram](https://github.com/Chordingg/ERD-/assets/157094467/598b4c49-0fb3-4e18-b2b8-152e161fcf0f)


***

[학사관리 시스템]

학생은 학번, 이름, 키, 학과코드로 이루어져 있습니다.
학과는 학과코드, 학과명으로 이루어져 있습니다.
교수는 교수코드, 교수명, 학과코드로 이루어져 있습니다.
개설과목은 과목코드, 과목명, 교수코드, 시작일, 종료일로 이루어져 있습니다.
수강은 학번, 과목코드로 이루어져 있습니다.

학과는 많은 학생을 가질 수 있고, 학생을 한 학과에 소속된다.
학과는 많은 교수를 가질 수 있고, 과목은 강의하는 교수 한 명이 지정된다.
과목은 수강하는 많은 학생을 가지고 학생은 많은 과목을 수강할 수 있다.

<객체 정의서>

객체명 속성명
학생  (학생, 이름, 키)
학과  (학과코드, 학과명)
교수  (교수코드, 교수명)
과목  (과목코드, 과목명, 시작일, 종료일)


|    |<center>참여객체/관계유형</center>|<center>속성</center>|
|----|---------------------:|:--------------------|
|소속|  학과  / 학생   |1 : N              
|    |  학과 / 교수   |1 : N            


|    |<center>참여객체/관계유형</center>|<center>속성</center>|
|----|---------------------:|:--------------------|
|강의|  교수 / 과목    |1 : N              
|수강|  학생 / 과목    |M : N   
