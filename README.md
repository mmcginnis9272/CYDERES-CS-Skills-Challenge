![alt text](https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/Horizontal-Lockup---Color.png)



   

<head>
<meta http-equiv=Content-Type content="text/html; charset=utf-8">
<meta name=ProgId content=Word.Document>
<meta name=Generator content="Microsoft Word 15">
<meta name=Originator content="Microsoft Word 15">
<link rel=File-List
href="CYDERES%20Customer%20Success%20Engineer%20challenge.fld/filelist.xml">

</head>

<body lang=EN-US style='tab-interval:.5in;word-wrap:break-word'>

<div class=WordSection1>

<p class=MsoNormal align=center style='text-align:center;tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><b><span style='font-size:24.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica'>CYDERES Customer Success
Engineer challenge<o:p></o:p></span></b></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica'>For the CYDERES Customer
Success Engineer challenge, I was provided the following “Security Log Data <span
class=GramE>“ to</span> ingest in to Logstash:</span><span style='font-family:
Helvetica;mso-bidi-font-family:Helvetica'><o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-family:Helvetica;
mso-bidi-font-family:Helvetica'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='mso-layout-grid-align:none;text-autospace:none'><span
style='font-size:18.0pt;font-family:"Courier New";color:black'>&lt;14&gt;1
2016-12-25T09:03:52.754646-06:00 contosohost1 antivirus 2496 - -&nbsp;<span
class=SpellE>alertname</span>=&quot;Virus Found&quot;&nbsp;<span class=SpellE>computername</span>=&quot;contosopc42&quot;&nbsp;<span
class=SpellE>computerip</span>=&quot;216.58.194.142&quot;
severity=&quot;1&quot;&nbsp;</span><span style='font-size:14.0pt;font-family:
"Courier New";color:black'><o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-family:Helvetica;
mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>I
wrote this data to the file <b>testdata.lo</b>g and placed it in the <span
class=SpellE><b>logstas</b>h</span> directory.<span style='mso-spacerun:yes'> 
</span>I then used the “<b>file</b>” Logstash input plugin in my <span
class=SpellE><b>test.conf</b></span><b> </b>file.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>
Initially, I chose the <b>grok</b> Logstash filter plugin to transform the
data.<span style='mso-spacerun:yes'>  </span>After a few hours of battling issues
with getting certain grok patterns to match correctly against data within quotes (ahh,
the days I’ve spent trying to “escape” quotes), I decided to try the <b>dissect</b>
filter. This turned out to be a much simpler approach as I will describe here:<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>The
<span class=GramE><b>dissect</b><span style='mso-spacerun:yes'>  </span>filter</span>
was used to break the log into fields by using the &lt;space&gt; character
between each field.<span style='mso-spacerun:yes'>  </span>The “description”
field (<span class=SpellE>alertname</span><span class=GramE>=“</span>Virus
Found” broke in to 2 parts due to a &lt;space&gt; character, so I appended
them together with the ‘+’ operator.<span style='mso-spacerun:yes'> 
</span>Since I only had a single log entry to work with; I can only assume this
might present problems if further log entries have more or less than 2 words
in this field.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>I
also added a few more fields than required, such as timestamp, site, service,
and port.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>I
then used the <span class=SpellE><b>remove_field</b></span> filter to remove
all the extra data fields that Logstash created without asking it to, like
host, original, event, log, etc.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>Then
I used the <b>mutate</b> filter to split the <span class=SpellE>source_ip</span>,
description, hostname, and security fields at the ‘<span class=GramE>=‘
character</span>, and assigned the field back to the right side ([1] array) of
each. Then I used the <span class=SpellE><b>gsub</b></span> filter to remove
those dreaded backslashes before the quotes in each field.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>Finally,
I used <span class=SpellE><b>gsub</b></span> once again on the severity field
to replace “1” with “High” and I <span class=GramE>made the assumption</span>
that “0” in this location should be replaced with “Low”.<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'>Here
is the output captured by <span class=SpellE>logstash</span> in both <span
class=SpellE><b>stdout</b></span> and <span class=SpellE><b>json</b></span>:</span><span
style='font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:
.5pt'><o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:.5in 1.0in 1.5in 2.0in 2.5in 3.0in 3.5in 4.0in 4.5in 5.0in 5.5in 6.0in;
mso-layout-grid-align:none;text-autospace:none'><span style='font-family:Helvetica;
mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>{<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>       </span>&quot;severity&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;High&quot;</span><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>        </span>&quot;service&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;antivirus&quot;</span><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>           </span>“site&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;contosohost1&quot;</span><span style='font-size:
18.0pt;font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>      </span>&quot;timestamp&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;2016-12-25T09:03:52.754646-06:00&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>      </span>&quot;<span class=SpellE><span
class=GramE>source</span>_ip</span>&quot;</span><span style='font-size:18.0pt;
font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'> =&gt; </span><span
style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;mso-font-kerning:.5pt'>&quot;216.58.194.142&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>    </span>&quot;description&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;Virus Found&quot;</span><span style='font-size:
18.0pt;font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>       </span>&quot;hostname&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;contosopc42&quot;</span><span style='font-size:
18.0pt;font-family:Menlo;color:black;mso-font-kerning:.5pt'>,<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><span
style='mso-spacerun:yes'>           </span>&quot;port&quot;</span><span
style='font-size:18.0pt;font-family:Menlo;color:#C7C7C7;mso-font-kerning:.5pt'>
=&gt; </span><span style='font-size:18.0pt;font-family:Menlo;color:#AAAB25;
mso-font-kerning:.5pt'>&quot;2496&quot;</span><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>}<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>{&quot;severity&quot;:&quot;High&quot;,&quot;service&quot;:&quot;antivirus<span
class=GramE>”,site</span>”:contosohost1&quot;,&quot;timestamp&quot;:&quot;2016-12-25T09:03:52.754646-06:00&quot;,&quot;source_ip&quot;:&quot;216.58.194.142&quot;,&quot;description&quot;:&quot;Virus
Found&quot;,&quot;hostname&quot;:&quot;contosopc42&quot;,&quot;port&quot;:&quot;2496&quot;}</span><span
style='font-family:Helvetica;mso-bidi-font-family:Helvetica;mso-font-kerning:
.5pt'><o:p></o:p></span></p>

   <p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'>Files of value included in this
repo:<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><a
href="https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/README.md">README.md</a>
– This file<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><a
href="https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/json_output.png">json_output.png</a>
– <span class=SpellE>Logstash</span> output in <span class=SpellE>json</span>
format<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><a
href="https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/stdout_output.png">stdout_output.png</a>
– Logstash output in <span class=SpellE>stdout</span> format <o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><a
href="https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/test.conf"><span
class=SpellE>test.conf</span></a> – Logstash configuration file<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><a
href="https://github.com/mmcginnis9272/CYDERES-CS-Skills-Challenge/blob/main/testdata.log">testdata.log</a>
– Security Log Data to be normalized<o:p></o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-size:18.0pt;
font-family:Menlo;color:black;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal style='tab-stops:28.0pt 56.0pt 84.0pt 112.0pt 140.0pt 168.0pt 196.0pt 224.0pt 3.5in 280.0pt 308.0pt 336.0pt;
mso-layout-grid-align:none;text-autospace:none'><span style='font-family:Helvetica;
mso-bidi-font-family:Helvetica;mso-font-kerning:.5pt'><o:p>&nbsp;</o:p></span></p>

<p class=MsoNormal><o:p>&nbsp;</o:p></p>


</div>

</body>

</html>
