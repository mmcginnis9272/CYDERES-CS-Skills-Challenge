![alt text](https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/Horizontal-Lockup---Color.png)

<html>
       <head><h># CYDERES-CS-Skills-Challenge</h></head>
       <title>CYDERES Customer Success skills challenge test.</title>
For the CYDERES Customer Success Engineer challenge, I was provide the following “Security Log Data “ to ingest in to Logstash:

<14>1 2016-12-25T09:03:52.754646-06:00 contosohost1 antivirus 2496 - - alertname="Virus Found" computername="contosopc42" computerip="216.58.194.142" severity="1" 

I wrote this data in a file called testdata.log and placed it in the logstash directory.  I then used the “file” Logstash input plugin in my test.conf file.

I originally chose the grok Logstash filter plugin to transform the data.  After a few hours battling issues getting some grok patterns to match correctly against data within quotes (ah, the days I’ve spent trying to “escape” quotes), I decided to try the dissect filter.
This turned out to be a much simpler approach as I will describe here:

The dissect  filter was used to break the log in to fields by using the <space> character between each field.  The “description” field (alertname=“Virus Found” broke in to 2 parts due to the <space> character, so I appended them together with the ‘+’ operator.  Since I only had a single log entry to work with, I can only assume this could present problems with further log entries have more or less than 2 words in this field.
I also added a few more fields than required such as timestamp, site, service, and port.

I then used the remove_field filter to remove all the extra data fields that Logstash created without asking it to, like host, original, event, log, etc.

Then I used the mutate filter to split the source_ip, description, hostname and security fields at the ‘=‘ character, and assigned the field back to the right side ([1] array) of each. Then I used the gsub filter to remove those dreaded backslashes before the quotes in each field.
Finally, I used gsub once again on the severity field to replace “1” with “High” and I made the assumption that “0” in this location should be replaced with “Low”.

Here is the output captured by logstash in both stdout and json:

[2022-05-20T23:11:49,493][INFO ][filewatch.observingtail  ][main][07978e95e9c9d70e9bfeeb3063206e9541a5b4ebd34029dac712e01dadb77acb] START, creating Discoverer, Watch with file and sincedb collections
{
       "severity" => "High",
        "service" => "antivirus",
           “site" => "contosohost1",
      "timestamp" => "2016-12-25T09:03:52.754646-06:00",
      "source_ip" => "216.58.194.142",
    "description" => "Virus Found",
       "hostname" => "contosopc42",
           "port" => "2496"
}

[2022-05-20T23:19:58,694][INFO ][logstash.agent           ] Pipelines running {:count=>1, :running_pipelines=>[:main], :non_running_pipelines=>[]}
{"severity":"High","service":"antivirus”,site”:contosohost1","timestamp":"2016-12-25T09:03:52.754646-06:00","source_ip":"216.58.194.142","description":"Virus Found","hostname":"contosopc42","port":"2496"}
       </html>
       <p>![visitors](https://visitor-badge.glitch.me/badge?page_id=${mmcginnis9272}.${mmcginnis9272@gmail.com})</p>
