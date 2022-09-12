# Stenography-Stenoread-Commands
### The files below are output to the /nsm/pcapout directory on Security Onion. This is mapped to the so-steno container's /tmp directory.

Search through stenographer files and index looking for all GRE traffic and write to pcap file. Will be saved in /nsm/pcaptmp/ directory.
<pre><code>docker container exec so-steno stenoread --limit-bytes 500000 'ip proto 47' -w /tmp/gre.pcap</code></pre>

The files below are output to the /nsm/pcapout directory. This is mapped to the so-steno container's /tmp directory.

Export the first 100 packets from 1 hour ago up to 30 minutes ago.
<pre><code>docker container exec so-steno stenoread --limit-packets 100 'before 30m ago and after 60m ago' -w /tmp/30m.pcap</code></pre>

Export the first 100 packets after 10:00Z on September 9, 2022 up to 10:59Z on September 9, 2022.
<pre><code>docker container exec so-steno stenoread --limit-packets 100 'before 2022-09-05T11:00:00Z and after 2022-09-05T10:00:00Z' -w /tmp/test.pcap</code></pre>

Print HTTP/HTTPS packet traffic between 4am and 5am on September 7, 2022 to the console
<pre><code>docker container exec so-steno stenoread 'before 2022-09-07T05:00:00Z and after 2022-09-07T04:00:00Z' -n 'tcp port 80 or tcp port 443'</code></pre>

Export packets within the last 15 minutes with the host ip 192.168.20.20. With the -n option, pass the output to tcpdump filtering for snmp (port 161) traffic.
<pre><code>docker container exec so-steno stenoread 'host 192.168.20.20 and after 15m ago' -n 'udp port 161' -w /tmp/snmp.pcap</code></pre>

Export packets starting 30 minutes ago and later between hosts 192.168.20.20 and 192.168.10.10. Use the -n option to pass to tcpdump and filter for SYN packets only.
<pre><code>docker container exec so-steno stenoread 'host 192.168.20.20 and host 192.168.10.10 and before 30m ago' -n 'tcp[13] == 2'</code></pre>

Export packets starting 30 minutes ago and later. Use the -n option to pass to tcpdump and filter for ACK packets only.
<pre><code>docker container exec so-steno stenoread 'before 30m ago' -n 'tcp[13] == 16'</code></pre>

Export packets starting 30 minutes ago and later. Use the -n option to pass to tcpdump and filter for SYN-ACK packets only.
<pre><code>docker container exec so-steno stenoread 'before 30m ago' -n 'tcp[13] == 18'</code></pre>
