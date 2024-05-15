# wehelp_week5

# Task2
Create database website;
use website;
create table member(
	id bigint primary key auto_increment,
    name varchar(255) not null,
    username varchar(255) not null,
    password varchar(255) not null,
    follower_count int unsigned not null default 0,
    time datetime not null default current_timestamp
);

# Task3
### insert new row set to be 'test'

insert into member(name, username, password) value('test', 'test', 'test');
insert into member(name, username,password,follower_count) value ('Chris1','christest',1234,103),('Tina2', 'tinatest',1234,567),('Harry3', 'harrytest',3456,222),("test",'test',1234,13);
select*from member;
select*from member order by time DESC;
select* from member order by time DESC limit 3 offset 1;
select*from member where name='test';
select*from member where name like '%es%';
explain select*from member where name like '%es%';
select*from member where username='test'and password='test';
SET SQL_SAFE_UPDATES=0;
update member set name='test2' where username='test';

# Task4
select count(id) from member;
select sum(follower_count) from member;
select avg(follower_count) from member;
select avg(follower_count) from 
(select follower_count from member order by follower_count desc limit 2) as top_followers;


# Task5
### message table
create table message(
 id bigint primary key auto_increment,
 member_id bigint not null, foreign key (member_id) references member(id),
 content varchar(255) not null,
 like_count int unsigned not null default 0,
 time datetime not null default current_timestamp
 );
select*from message;

### data insert to message table
insert into message (member_id, content, like_count) value(1, 'words',33);
insert into message (member_id, content, like_count) value(1, 'second test',43);
insert into message (member_id, content, like_count) value(2, 'hey',23);
insert into message (member_id, content, like_count) value(2, 'wer',12345);
insert into message (member_id, content, like_count) value(3, 'you',4);
insert into message (member_id, content, like_count) value(4, 'learning is hard work',44);
### 合併資料
SELECT member.name AS sender_name,message.id as message_id, message.member_id, message.content, message.like_count, message.time
FROM message
INNER JOIN member ON message.member_id = member.id;

### 篩選usernmae=test
select 
	member.username, 
    message.id as message_id, 
    member.name as sender_name, 
    message.member_id, 
    message.content, 
    message.like_count,
    message.time
from message 
right join member on message.member_id=member.id 
where member.username='test';
### get the average like count of message where sender username equal to test

select 
	member.username,
    avg(message.like_count)
from message 
join member on message.member_id=member.id 
where member.username='test'
;
### get the average like count of messages group by sender username
select 
	member.username,
    avg(message.like_count)
from message
join member on message.member_id=member.id
group by member.username;
show tables;

