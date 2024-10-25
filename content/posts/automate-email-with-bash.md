+++ 
date = 2024-10-24T02:20:18+01:00
title = "Automate Sending Email Through Gmail with Bash Script"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

## Setting an App Password

- Click on the top-right icon -> Manage your Google Account -> Search `app password` on the search bar -> Sign in with App Password
- Follow the steps and eventually you will be given a app password that look something like this: `aaaa bbbb cccc dddd`

## Bash script

- Use the following script to verify that the sending of email works (don't forget to `chmod +x`):

```bash
#!/bin/bash

# Prompt the user for input
read -p "Enter your email: " sender
read -p "Enter recipient email: " receiver
read -s -p "Enter your Google App password: " gapp
echo
read -p "Enter the subject of mail: " sub

# Read the body of the email
echo "Enter the body of mail (Ctrl+D to end):"
body=$(</dev/stdin)

# Sending email using curl
response=$(curl -s --url 'smtps://smtp.gmail.com:465' --ssl-reqd \
    --mail-from "$sender" \
    --mail-rcpt "$receiver" \
    --user "$sender:$gapp" \
    -T <(echo -e "From: $sender\nTo: $receiver\nSubject: $sub\n\n$body"))

if [ $? -eq 0 ]; then
    echo "Email sent successfully."
else
    echo "Failed to send email."
    echo "Response: $response"
fi
```

## Modify Bash Script

- Modify the bash script to suit your need, for e.g:

```bash
#!/bin/bash

# for error handling when running cronjob, save output to log.txt
printf "\n$(date) \n" >>log.txt
exec >>log.txt 2>&1

MEETING_DATE=$(date -d "+2 days" +'%m/%d/%Y') # set date 2 days from now
RECIPIENTS_FORMATTED=""
RECIPIENTS="email1@abc.com email2@abc.com"

# prepend all recipient's email with "--mail-rcpt", for e.g: "--mail-rcpt email1@abc.com --mail-rcpt email2@abc.com"
for i in $RECIPIENTS
do
RECIPIENTS_FORMATTED+="--mail-rcpt $i "
done

response=$(curl -s --url 'smtps://smtp.gmail.com:465' --ssl-reqd \
    --mail-from "email-address-to-send-from@gmail.com" $RECIPIENTS_FORMATTED \
    --user "email-address-to-send-from@gmail.com:aaaa bbbb cccc dddd" \
    -T <(echo -e "From: email-address-to-send-from@gmail.com\nTo: $RECIPIENTS\nSubject: Agenda for our meeting 1:00pm-2:00pm on Thursday ($MEETING_DATE)\n\nHi,\n\nPlease find the agenda as follows:\n13:00-13:15: Alice's update.\n13:15-13:30: Bob's update.\n13:30-13:45: Charlie's update.\n13:45-14:00: Discussions: miscellaneous.\n\nhttps://teams.microsoft.com/l/meetup-join/19%3_NzZjZGXiOTYtMDRiOS00ZmI0-random-meeting-link\n\nRegards,\nUsername"))

if [ $? -eq 0 ]; then
    echo "Email sent successfully."
else
    echo "Failed to send email."
    echo "Response: $response"
fi
```

- multiple line of `--mail-rcpt` for multiple recipients.
- `aaaa bbbb cccc dddd` refers to the app password.

## Setup Cronjob

- Setup crontab with `crontab -e`:
- E.g. at 12pm on Thursday: `0 12 * * 4`
- Use: https://crontab.guru/

# Ref

https://www.fosstechnix.com/how-to-send-email-using-shell-script/
