UFM SDK
--------------------------------------------------------

This is the UFM SDK.
It allows streaming UFM APIs to fluentd endpoint 

Prerequisites 
--------------------------------------------------------

The following python packages are required to run this app:

>requests

>configparser

>json

>logging

>FluentSender

Configuration  
-------------------------------------------------------- 
Please modify sdk.cfg file to set the Fluentd and UFM parameters.

Run  
-------------------------------------------------------- 
python app.py

Use  
-------------------------------------------------------- 
This application is not a daemon; you should run it via time-based job scheduler (cron job).
