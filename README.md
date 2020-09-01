# AzureDataFactory SCD Type 1 implementation in Azure Cloud Platform
## Create table statements
### Insert & Update table statements
##### Visit Medium blog to understand the concept : https://medium.com/@apu.nandi88/concept-and-scd-type-1-implementation-in-azure-cloud-data-warehouse-c493ab374458
----------------- craete product_table -----------------------[Source] 
create table dbo.product_table( product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int,
Sync_Flag int
);

----------------- craete product_dim_stg -----------------------[Target] 
create table dbo.product_dim_stg( product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int
);
----------------- craete product_dim -----------------------[Target] 
create table dbo.product_dim( product_key int,
product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int,
added_date datetime,
updated_date datetime
);

------------------------- 1st Run insert data into source product_table-----------------------------------------------------------------------------------------------
insert into dbo.product_table values(100,'Sony LED TV 40"',25999.00,'Sony 101.6 cm (40 inch) Full HD LED TV, KLV-40R252F',1,0);
insert into dbo.product_table values(101,'LG 5 starMicrowave',12890.00,'LG 28 litres Convection Microwave Oven, MC2846SL',0,0);
insert into dbo.product_table values(102,'Dell HD Monitor',8999.00,'DELL 19.5-inch HD Monitor - D2020H',1,0);
insert into dbo.product_table values(103,'Philips Iron',1299.49,'Philips GC3920/24 Steam Iron',0,0);

-------------------- 2nd Run insert and update data into source product_table-----------------------------------------------------------------------------------------------------
update dbo.product_table set unit_price=9999.00,eligible_promotion=0,Sync_Flag=0 where product_id=102;
update dbo.product_table set unit_price=1095.50,eligible_promotion=1,Sync_Flag=0 where product_id=103;
insert into dbo.product_table values(104,'Philips Beard Trimmer',2199.00,'Philips BT3221/15 corded & cordless Titanium blade Beard Trimmer - 20 length settings; 90 min run time',0,0);

