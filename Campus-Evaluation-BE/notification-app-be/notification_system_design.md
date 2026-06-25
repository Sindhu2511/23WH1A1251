Basic Requirements: REST API Design, contract and structure to display notifications to the users when they are logged in

Stage 1:
Core Actions:
    -> Send Notifications
    -> Receive Notifications
    -> Delete Notifications

1. Send Notifications
HTTP Method: POST
Method Name: notify_others
JSON Request: 
{
    "sender" : "ramakrishna",
    "receiver" : "sindhu",
    "message-type" : "mail updates",
    "message" : "I got your mail",
    "is-read" : "False"
}
JSON Response:
{
    "sender" : "ramakrishna"
    "date-and-time" : "25/06/2026 14:48:45",
    "message-type" : "mail update",
    "message" : "I got your mail",
    "is-read" : "True"
}
Authorization: Only authorized personnel can send messages after entering their authorized key / the password. 
They Kay must be selected as Authorization and in value, they must add the Key / Password.

2. Receive Notifications
HTTP Method: GET
Method Name: notifications
JSON Request:
{
    "sender" : "ramakrishna"
    "date-and-time" : "25/06/2026 14:48:45",
    "message-type" : "mail update",
    "message" : "I got your mail",
    "is-read" : "False"
}
{
    "sender" : "prabha"
    "date-and-time" : "24/06/2026 14:48:45",
    "message-type" : "project plan",
    "message" : "Here is the attached project plan, let us proceed with this idea",
    "is-read" : "False"
}
Authorization: Only authorized personnel can recieve messages after entering their authorized key / the password. 
They Kay must be selected as Authorization and in value, they must add the Key / Password.

3. Delete Notifications
HTTP Method: DELETE
Method Name: delete_notification
JSON Request:
{
    "sender" : "ramakrishna"
    "date-and-time" : "25/06/2026 14:48:45",
    "message-type" : "mail update",
    "message" : "I got your mail",
    "is-read" : "True"
}

Authorization: Only authorized personnel can delete messages after entering their authorized key / the password. 
They Kay must be selected as Authorization and in value, they must add the Key / Password.

Stage 2:
Better DB Choice: Relational DB. 
Reasoning: Relational Databases store in the form of rows and columns. Any information we have, can be stored as rows and columns in a structured way to prevent any kind of future errors. 
The problem that could arise when the data volume increases could be accessing huge amount of data at once. Such problems can be easily solved using indexing. 
Notification Message:

CREATE notifications;
USE notifications;
CREATE TABLE message(
    id integer auto_increment primary key,
    sender varchar(100),
    message-type varchar(200),
    receiver varchar(100),
    message text,
    date_time datetime,
    isread boolean
);

Stage 3:

End Goal: Fetch all unread notifications of a student

Yes, the query is accurate.
The reason it is slow:
There are around 5 milion students. Each student can get many messages per day, due to which there can be many un read as well. So running through the database to find them is hard. 

Yes, indexes are the solution for this. These are used for easy and fast retrieval of values. 

select * from notifications where notification_type == 'Result' where message like '%Passed%' and date_time >= now() - internal 7 day;

Stage 4
Instead of fetching the notifications for each page load, keep a cache memory that keeps the last fetched page load and returns it if there are no new messages. 

The problem with this approach is, even though it would be fast, it would need a lot of extra / additional memory. This new memory will be more expensive. 

Stage 5

Problem: It should send to all 50,000 students an email at once, but instead, it failed after it reached the 200 mark. 
Reason: Because it calls three functions at once, and these three functions when called at once, take significantly more time. 
Instead of doing these three works all at once, we can do it twice. 

First time, we will send the email to all the students at once, and push the notification to the app. 
Next we will store all of it in our databases. 

function notify_all(student_ids: array, message: string):
    for student_id in student_ids:
        send_email(student_id, message)
        push_to_app(student_id, message)

function notify_all(student_ids: array, message: string):
    for student_id in student_ids:
        save_to_db(student_id, message)

