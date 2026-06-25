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
    "message" : "I got your mail"
}
JSON Response:
{
    "sender" : "ramakrishna"
    "date-and-time" : "25/06/2026 14:48:45",
    "message-type" : "mail update",
    "message" : "I got your mail"
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
    "message" : "I got your mail"
}
{
    "sender" : "prabha"
    "date-and-time" : "24/06/2026 14:48:45",
    "message-type" : "project plan",
    "message" : "Here is the attached project plan, let us proceed with this idea"
}
Authorization: Only authorized personnel can recieve messages after entering their authorized key / the password. 
They Kay must be selected as Authorization and in value, they must add the Key / Password.

2. Receive Notifications
HTTP Method: DELETE
Method Name: delete_notification
JSON Request:
{
    "sender" : "ramakrishna"
    "date-and-time" : "25/06/2026 14:48:45",
    "message-type" : "mail update",
    "message" : "I got your mail"
}

Authorization: Only authorized personnel can delete messages after entering their authorized key / the password. 
They Kay must be selected as Authorization and in value, they must add the Key / Password.

Stage 2:
