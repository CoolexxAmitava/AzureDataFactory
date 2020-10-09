# AzureDataFactory
# SCD Type 2
# Slow Changing Dimension Type 2 and Type 4 Concept and Implementation
#
----------------- craete product_table -----------------------[Source Table] 
create table dbo.product_table( product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int,
created_date datetime,
Sync_Flag int
);
select product_id,product_name,unit_price,product_desc,eligible_promotion from dbo.product_table where Sync_Flag=0;
----------------- craete product_dim_stg -----------------------[Target Table] 
create table dbo.product_dim_stg( product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int,
created_date datetime
);
----------------- craete product_dim -----------------------[Target Table] 
create table dbo.product_dim( product_key int,
product_id int not null,
product_name varchar(256),
unit_price float,
product_desc varchar(512),
eligible_promotion int,
start_date datetime,
end_date datetime,
active_flag int
);

------------------------- 1st Run insert data into source product_table-----------------------------------------------------------------------------------------------
insert into dbo.product_table values(100,'Sony LED TV 40"',25999.00,'Sony 101.6 cm (40 inch) Full HD LED TV, KLV-40R252F',1,getdate(),0);
insert into dbo.product_table values(101,'LG 5 starMicrowave',12890.00,'LG 28 litres Convection Microwave Oven, MC2846SL',0,getdate(),0);
insert into dbo.product_table values(102,'Dell HD Monitor',8999.00,'DELL 19.5-inch HD Monitor - D2020H',1,getdate(),0);
insert into dbo.product_table values(103,'Philips Iron',1299.49,'Philips GC3920/24 Steam Iron',0,getdate(),0);

-------------------- 2nd Run insert and update data into source product_table-----------------------------------------------------------------------------------------------------
update dbo.product_table set unit_price=9999.00,eligible_promotion=0,Sync_Flag=0 where product_id=102;
update dbo.product_table set unit_price=1095.50,eligible_promotion=1,Sync_Flag=0 where product_id=103;
insert into dbo.product_table values(104,'Philips Beard Trimmer',2199.00,'Philips BT3221/15 corded & cordless Titanium blade Beard Trimmer - 20 length settings; 90 min run time',0,getdate(),0);
