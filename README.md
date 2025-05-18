```mysql

create database library_system;

USE library_system;


drop table system_manage;
drop table system_book_manage;
drop table book_manage;
drop table borrow;
drop table user;
drop table system_administrator;
drop table book_administrator;
drop table book;
-- 图书表
create table book (
        book_id int auto_increment primary key,
        book_name varchar(20),
        author varchar(20),
        publisher varchar(20),
        publish_date date,
        type varchar(20),
        status enum('isBorrowed', 'notBorrowed') default 'notBorrowed'
);

create table book_administrator (
        admin_id int auto_increment primary key,
        admin_name varchar(20),
        admin_password varchar(20)
);

create table system_administrator (
        sysadmin_id int auto_increment primary key,
        sysadmin_name varchar(20),
        sysadmin_password varchar(20)
);

create table user (
         user_id int auto_increment primary key,
         username varchar(20),
         user_password varchar(20)
);

create table borrow (
         borrow_id int auto_increment primary key,
         book_id int not null,
         user_id int not null,
         administrator_id int not null,
         borrow_date date,
         should_return_date date,
         return_date date,
         foreign key (book_id) references book(book_id),
         foreign key (user_id) references user(user_id),
         foreign key (administrator_id) references book_administrator(admin_id)
);

create table book_manage (
           manage_id int auto_increment primary key,
           book_id int not null,
           manager_id int not null,
           foreign key (book_id) references book(book_id),
           foreign key (manager_id) references book_administrator(admin_id)
);

create table system_book_manage (
           sys_manage_id int auto_increment primary key,
           book_id int not null,
           manager_id int not null,
           foreign key (book_id) references book(book_id),
           foreign key (manager_id) references system_administrator(sysadmin_id)
);

create table system_manage (
            system_manage_id int auto_increment primary key,
            book_manager_id int not null,
            system_manager_id int not null,
            foreign key (book_manager_id) references book_administrator(admin_id),
            foreign key (system_manager_id) references system_administrator(sysadmin_id)
);


insert into book (book_name, author,publisher,publish_date, type, status) values
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



```