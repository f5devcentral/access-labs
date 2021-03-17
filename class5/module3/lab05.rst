
TCPDump 
===================================

Beginning in BIG-IP 11.2.0, you can use the “\ **p**\ ” interface
modifier with the “\ **p**\ ” modifier to capture traffic with TMM
information for a specific flow, and its related peer flow. The
“\ **p**\ ” modifier allows you to capture a specific traffic flow
through the BIG-IP system from end to end, even when the configuration
uses a Secure Network Address Translation (SNAT) or OneConnect. For
example, the following command searches for traffic to or from client
**10.128.10.100** on interface **0.0**:

**tcpdump -ni 0.0:nnnp -s0 -c 100000 -w /var/tmp/capture.dmp host
10.128.10.100**

Once **tcpdump** identifies a related flow, the flow is marked in TMM,
and every subsequent packet in the flow (on both sides of the BIG-IP
system) is written to the capture file.