create database library_system;

USE library_system;


drop table systemManage;
drop table systemBookManage;
drop table bookManage;
drop table borrow;
drop table user;
drop table systemAdministrator;
drop table bookAdministrator;
drop table book;
-- 图书表
create table book (
id int auto_increment primary key ,
name varchar(20),
author varchar(20),
publisher varchar(20),
publishDate date,
type varchar(20),
status enum('isBorrowed', 'notBorrowed') DEFAULT 'notBorrowed'
);


create table bookAdministrator(
id int auto_increment primary key ,
name varchar(20),
password varchar(20)
);

create table systemAdministrator(
id int auto_increment primary key ,
name varchar(20),
password varchar(20)
);

create table user(
id int auto_increment primary key ,
username varchar(20),
userCode varchar(20)
);

create table borrow(
id int auto_increment primary key ,
bookId int not null ,
userId int not null ,
administratorId int not null ,
borrowDate date ,
shouldReturnDate date,
returnDate date,
foreign key(bookId) references book(id),
foreign key(userId) references user(id),
foreign key(administratorId) references bookAdministrator(id)
);

create table bookManage(
id int auto_increment primary key,
bookId int not null ,
managerId int not null ,
foreign key(bookId) references book(id),
foreign key(managerId) references bookAdministrator(id)

);


create table systemBookManage(
id int auto_increment primary key,
bookId int not null ,
managerId int not null ,
foreign key(bookId) references book(id),
foreign key(managerId) references systemAdministrator(id)
);

create table systemManage(
id int auto_increment primary key,
bookManagerId int not null ,
systemManagerId int not null ,
foreign key(bookManagerId) references bookAdministrator(id),
foreign key(systemManagerId) references systemAdministrator(id)
);


insert into book (name, author, publisher, publishDate, type, status) values
('三体', '刘慈欣', '重庆出版社', '2008-01-01', '科幻', 'notBorrowed'),
('平凡的世界', '路遥', '人民文学出版社', '1986-12-01', '文学', 'notBorrowed'),
('活着', '余华', '作家出版社', '1993-06-01', '文学', 'notBorrowed'),
('Java编程思想', 'Bruce Eckel', '机械工业出版社', '2007-06-01', '计算机', 'notBorrowed'),
('Python基础教程', 'Magnus Lie Hetland', '人民邮电出版社', '2018-02-01', '计算机', 'notBorrowed'),
('百年孤独', '加西亚·马尔克斯', '南海出版公司', '2011-06-01', '外国文学', 'notBorrowed'),
('白夜行', '东野圭吾', '南海出版公司', '2013-01-01', '推理', 'notBorrowed'),
('小王子', '圣埃克苏佩里', '人民文学出版社', '2003-08-01', '童话', 'notBorrowed'),
('围城', '钱钟书', '人民文学出版社', '1991-02-01', '文学', 'notBorrowed'),
('人类简史', '尤瓦尔·赫拉利', '中信出版社', '2017-02-01', '历史', 'notBorrowed'),
('数据结构与算法', '严蔚敏', '清华大学出版社', '2020-05-01', '计算机', 'notBorrowed'),
('红楼梦', '曹雪芹', '人民文学出版社', '1996-12-01', '古典文学', 'notBorrowed'),
('时间简史', '史蒂芬·霍金', '湖南科技出版社', '2010-04-01', '科普', 'notBorrowed'),
('追风筝的人', '卡勒德·胡赛尼', '上海人民出版社', '2006-05-01', '外国文学', 'notBorrowed'),
('Effective Java', 'Joshua Bloch', '机械工业出版社', '2019-01-01', '计算机', 'notBorrowed'),
('明朝那些事儿', '当年明月', '中国友谊出版公司', '2009-04-01', '历史', 'notBorrowed'),
('挪威的森林', '村上春树', '上海译文出版社', '2001-02-01', '外国文学', 'notBorrowed'),
('设计模式', 'Erich Gamma', '机械工业出版社', '2021-03-01', '计算机', 'notBorrowed'),
('沉默的大多数', '王小波', '中国青年出版社', '1997-10-01', '杂文', 'notBorrowed'),
('天龙八部', '金庸', '生活·读书·新知三联书店', '1994-05-01', '武侠', 'notBorrowed');


