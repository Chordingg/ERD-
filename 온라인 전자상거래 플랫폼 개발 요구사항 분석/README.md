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

***

##### 👉 [객체 관계 정의서]

|객체명|속성명|||||||관계유형|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|고객|고객코드|고객명|전화번호|이메일|주소(기본,상세)|지역|가입일
|지역|지역코드|지역명|
|제품|제품코드|제품명|가격|
|----|----|----|----|----|----|----|----|----|
|구매|구매코드|구매수량|구매일자|||||M : N 
|관리|고객은 지역별로 관리|||||||1 : N 

***

🔹 테이블 정의서

![테이블 정의서(excel)](https://github.com/Chordingg/ERD-/assets/157094467/aaf4241a-88db-4c10-8710-2c12e2f4964e)

</br>

🔹 개념적 모델링

![주석 2024-04-02 114042](https://github.com/Chordingg/ERD-/assets/157094467/0c84812e-62d5-42d1-883d-04b64a401aa8)

</br>

🔹 논리적 모델링

![주석 2024-04-02 114118](https://github.com/Chordingg/ERD-/assets/157094467/61e36240-86d6-44ab-ba4f-c16f67d40fa0)

</br>

🔹 EER Diagram

![MySQL EER Diagram](https://github.com/Chordingg/ERD-/assets/157094467/598b4c49-0fb3-4e18-b2b8-152e161fcf0f)

</br>

***

🔸 MySQL Workbench Forward Engineering

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8mb3 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`t_region`
-- -----------------------------------------------------

-- create the t_region table
CREATE TABLE t_region(
	region_code varchar(3) not null,
	region_name varchar(10) not null,
	primary key(region_code)
);

-- -----------------------------------------------------
-- Table `mydb`.`t_customer`
-- -----------------------------------------------------

-- Create the t_customer table
CREATE TABLE t_customer (
	customer_id int not null auto_increment,
	customer_name varchar(10) not null,
	phone varchar(20) not null 	unique,
	email varchar(50) not null	unique,
	address varchar(100) not null,
	regist_date datetime default now(),
	region_code varchar(3) not null,
	primary key(customer_id)
);

-- -----------------------------------------------------
-- Table `mydb`.`t_product`
-- -----------------------------------------------------

-- Create the t_product table
CREATE TABLE t_product(
	product_code int not null auto_increment,
	product_name  varchar(50) not null,
	price int,
	primary key(product_code)
);

-- -----------------------------------------------------
-- Table `mydb`.`t_sales`
-- -----------------------------------------------------

-- Create the t_sales table
CREATE TABLE t_sales(
	id int not null auto_increment,
	customer_id int not null,
	product_code int not null,
	qty int not null,
	sales_date datetime default now(),
	primary key(id)
);

ALTER TABLE t_customer
ADD CONSTRAINT fk_region_code FOREIGN KEY (region_code ) REFERENCES t_region(region_code);

ALTER TABLE t_sales
ADD CONSTRAINT fk_customer_id FOREIGN KEY (customer_id ) REFERENCES t_customer( customer_id),
ADD CONSTRAINT fk_product_code FOREIGN KEY (product_code ) REFERENCES t_product( product_code);

use mydb;
select * from t_region;
desc t_region;
-- t_region Å×ÀÌºí¿¡ µ¥ÀÌÅÍ Ãß°¡
INSERT INTO t_region (region_code , region_name ) VALUES
('02', '¼­¿ïÆ¯º°½Ã'),

('031', '°æ±âµµ'),
('032', 'ÀÎÃµ±¤¿ª½Ã'),
('033', '°­¿øÆ¯º°ÀÚÄ¡µµ'),
('041', 'ÃæÃ»³²µµ'),
('042', '´ëÀü±¤¿ª½Ã'),
('043', 'ÃæÃ»ºÏµµ'),
('044', '¼¼Á¾Æ¯º°ÀÚÄ¡½Ã'),
('051', 'ºÎ»ê±¤¿ª½Ã'),
('052', '¿ï»ê±¤¿ª½Ã'),
('053', '´ë±¸±¤¿ª½Ã'),
('054', '°æ»óºÏµµ'),
('055', '°æ»ó³²µµ'),
('061', 'Àü¶ó³²µµ'),
('062', '±¤ÁÖ±¤¿ª½Ã'),
('063', 'Àü¶óºÏµµ'),
('064', 'Á¦ÁÖÆ¯º°ÀÚÄ¡µµ');


-- t_customer Å×ÀÌºí¿¡ µ¥ÀÌÅÍ Ãß°¡

INSERT INTO t_customer (customer_name , phone, email, address, region_code)
VALUES
('È«±æµ¿ ', '010 1234 5678', 'hong@example.com', ' ¼­¿ï½Ã °­³²±¸', '02'),
('±èÃ¶¼ö ', '010 9876 5432', 'kim@example.com', ' °æ±âµµ ¼ö¿ø½Ã ', '031'),
('ÀÌ¿µÈñ ', '010 1111 2222', 'lee@example.com', ' ÀÎÃµ½Ã ³²±¸ ', '032'),
('¹Ú¹ÎÁö ', '010 5555 7777', 'park@example.com', ' °­¿øµµ ÃáÃµ½Ã ', '033'),
('Á¤±âÈ£ ', '010 9999 8888', 'jung@example.com', ' ´ëÀü½Ã Áß±¸ ', '042');


-- t_product Å×ÀÌºí¿¡ µ¥ÀÌÅÍ Ãß°¡
INSERT INTO t_product (product_name ,price)
values
('³ëÆ®ºÏ',1500000),
('½º¸¶Æ®Æù ', 1000000),
('Å°º¸µå ', 50000),
('¸¶¿ì½º ', 30000),
('ÀÌ¾îÆù ', 70000);


-- t_sales Å×ÀÌºí¿¡ µ¥ÀÌÅÍ Ãß°¡
INSERT INTO t_sales (customer_id , product_code , qty)
VALUES
(1, 1, 2),
(2, 2, 1),
(3, 3, 5),
(4, 4, 3),
(5, 5, 2),
(1, 2, 3),
(3, 1, 1),
(2, 4, 2),
(4, 3, 4),
(5, 5, 1);
