---
title: ContAInment
tags:
  - thm
  - medium
---

#### Author: AMD

![[static/containment/containment.webp]]


This is a writeup for <b>ContAInment</b> room.

-----------------------------------------------------------------------------------
<b>CONNECT</b>

Lets connect the workstation with ssh.

![[static/containment/connect.webp]]

-----------------------------------------------------------------------------------
<b>CHECK THE EMAILS</b>

![[static/containment/emls.webp]]

Lets analyze them by starting with the most recent one.

![[static/containment/prompt1.webp]]

Lets look at the email.

![[static/containment/email_content.webp]]

-----------------------------------------------------------------------------------
<b>FIND THE ATTACHMENT</b>

![[static/containment/find_scr.webp]]

Lets analyze it.

![[static/containment/scr_content.webp]]

It contains reverse shell to 10.0.0.42 on port 443

-----------------------------------------------------------------------------------
<b>FIND THE PCAP</b>

![[static/containment/find_pcap.webp]]

Lets go to the incident date with "cd /home/o.deer/Documents/pcap_dumps/2025-06-17"

Lets run the code below to find the .pcap we need to analyze.

```shell
for file in /home/o.deer/Documents/pcap_dumps/2025-06-17/*.pcap; do
  echo "Checking $file"
  tshark -r "$file" -q -z follow,tcp,ascii,0
done
```

Only /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap has an output.

![[static/containment/session_4444_dump.webp]]


-----------------------------------------------------------------------------------
<b>ANALYZE PCAP FILE</b>

Let's start with the recunstruction.

![[static/containment/prompt2.webp]]

Lets read /home/o.deer/qwen-output/reassembled_data_dump.txt

![[static/containment/session_4444_dump_content.webp]]

Can this be the password of teh .zip file

-----------------------------------------------------------------------------------
<b>UNZIP</b>

![[static/containment/unzip.webp]]

-----------------------------------------------------------------------------------
<b>GET THE FLAG</b>

Lets look at the guide.

![[static/containment/flags_guide.webp]]

Lets use AI again. 

![[static/containment/prompt3.webp]]
