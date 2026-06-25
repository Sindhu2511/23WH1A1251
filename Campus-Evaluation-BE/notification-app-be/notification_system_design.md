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

