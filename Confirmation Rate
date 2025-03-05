
CREATE TABLE Signups (
    user_id INT PRIMARY KEY,
    time_stamp DATETIME
);

CREATE TABLE Confirmations (
    user_id INT,
    time_stamp DATETIME,
    action ENUM('confirmed', 'timeout'),
    PRIMARY KEY (user_id, time_stamp),
    FOREIGN KEY (user_id) REFERENCES Signups(user_id)
);

INSERT INTO Signups (user_id, time_stamp) VALUES
(3, '2020-03-21 10:16:13'),
(7, '2020-01-04 13:57:59'),
(2, '2020-07-29 23:09:44'),
(6, '2020-12-09 10:39:37');

INSERT INTO Confirmations (user_id, time_stamp, action) VALUES
(3, '2021-01-06 03:30:46', 'timeout'),
(3, '2021-07-14 14:00:00', 'timeout'),
(7, '2021-06-12 11:57:29', 'confirmed'),
(7, '2021-06-13 12:58:28', 'confirmed'),
(7, '2021-06-14 13:59:27', 'confirmed'),
(2, '2021-01-22 00:00:00', 'confirmed'),
(2, '2021-02-28 23:59:59', 'timeout');



with count_test as ( 
select s.user_id ,count( c.user_id ) total_request ,
sum( case when c.action='confirmed' then 1 else 0 end ) as confirmed_request 
from Signups s 
left join Confirmations  c
on s.user_id = c.user_id
group by s.user_id) 

select  user_id ,
ifnull ( round ( confirmed_request / total_request , 2) , 0) as confirmation_rate
from count_test 
