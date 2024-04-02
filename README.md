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

</br>

##### 👉 [객체 관계 정의서]

|객체명|속성명|||||||관계유형|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|고객|고객코드|고객명|전화번호|이메일|주소(기본,상세)|지역|가입일
|지역|지역코드|지역명|
|제품|제품코드|제품명|가격|
|----|----|----|----|----|----|----|----|----|
|구매|구매코드|구매수량|구매일자|||||M : N 
|관리|고객은 지역별로 관리|||||||1 : N 

</br>

🔹 개념적 모델링

![주석 2024-04-02 114042](https://github.com/Chordingg/ERD-/assets/157094467/0c84812e-62d5-42d1-883d-04b64a401aa8)

</br>

🔹 논리적 모델링

![주석 2024-04-02 114118](https://github.com/Chordingg/ERD-/assets/157094467/61e36240-86d6-44ab-ba4f-c16f67d40fa0)

</br>

🔹 EER Diagram

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

</br>

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

</br>

🔹 개념적 모델링

![주석 2024-04-02 104426](https://github.com/Chordingg/ERD-/assets/157094467/1dc4e897-8ef0-4ed6-96c5-48d48ca55452)

</br>

🔹 논리적 모델링

![주석 2024-04-02 115105](https://github.com/Chordingg/ERD-/assets/157094467/350b0700-469b-4035-a649-494e23c4d37b)

</br>

🔹 EER Diagram

![주석 2024-04-02 115828](https://github.com/Chordingg/ERD-/assets/157094467/8b3ed933-b616-44d0-bf52-9094967ba4d6)

</br>
</br>

🔸 MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8mb3 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`department`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`department` (
  `department_code` INT NOT NULL,
  `department_name` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`department_code`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`student`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`student` (
  `student_id` INT NOT NULL,
  `student_name` VARCHAR(50) NOT NULL,
  `student_height` DECIMAL(5,2) NULL,
  `department_department_code` INT NOT NULL,
  PRIMARY KEY (`student_id`),
  INDEX `fk_student_department_idx` (`department_department_code` ASC) VISIBLE,
  CONSTRAINT `fk_student_department`
    FOREIGN KEY (`department_department_code`)
    REFERENCES `mydb`.`department` (`department_code`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`professor`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`professor` (
  `professor_code` INT NOT NULL,
  `professor_name` VARCHAR(50) NOT NULL,
  `department_department_code` INT NOT NULL,
  PRIMARY KEY (`professor_code`),
  INDEX `fk_professor_department1_idx` (`department_department_code` ASC) VISIBLE,
  CONSTRAINT `fk_professor_department1`
    FOREIGN KEY (`department_department_code`)
    REFERENCES `mydb`.`department` (`department_code`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`course`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`course` (
  `course_code` INT NOT NULL,
  `course_name` VARCHAR(50) NOT NULL,
  `start_date` DATE NULL,
  `end_date` DATE NULL,
  `professor_professor_code` INT NOT NULL,
  PRIMARY KEY (`course_code`),
  INDEX `fk_course_professor1_idx` (`professor_professor_code` ASC) VISIBLE,
  CONSTRAINT `fk_course_professor1`
    FOREIGN KEY (`professor_professor_code`)
    REFERENCES `mydb`.`professor` (`professor_code`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`student_course`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`student_course` (
  `id` INT NOT NULL,
  `student_student_id` INT NOT NULL,
  `course_course_code` INT NOT NULL,
  INDEX `fk_student_course_student1_idx` (`student_student_id` ASC) VISIBLE,
  INDEX `fk_student_course_course1_idx` (`course_course_code` ASC) VISIBLE,
  UNIQUE INDEX `id_UNIQUE` (`id` ASC) VISIBLE,
  PRIMARY KEY (`course_course_code`, `student_student_id`),
  CONSTRAINT `fk_student_course_student1`
    FOREIGN KEY (`student_student_id`)
    REFERENCES `mydb`.`student` (`student_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_student_course_course1`
    FOREIGN KEY (`course_course_code`)
    REFERENCES `mydb`.`course` (`course_code`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
