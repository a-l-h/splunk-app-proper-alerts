Prerequisites
============

The follwoing Apps must be deployed to your Search Head(s)
- Gemini KV Store Tools: https://splunkbase.splunk.com/app/3536/
- Python Cron Iteration for Splunk: https://splunkbase.splunk.com/app/4027/
- Lookup File Editor: https://splunkbase.splunk.com/app/1724/
- Lookup File Editor: https://splunkbase.splunk.com/app/1724/

1 - Install the App on your Splunk Search Head(s).

2 - Launch 'Update KV Store lookup' to populate KV Store lookup. 
    To do so you can edit alert's cron schedule to the next minute and wait for it to be triggerred.

3 - Go to Inventory dashboard to verify data is here

4 - Adjust 'Update KV Store Lookup' cron schedule as needed (once a day, once an hour...)

5 - Optional - When ready, enable this Notify alert owner of a change

6 - Optional - When ready, adjust email for Notify admin for alerts to review and enable
