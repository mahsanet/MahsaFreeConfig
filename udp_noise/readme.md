## udp noise

#### introduced 2024-Q4 by @mmmray
 
1. chain udp config outbound to freedom using sockopt
2. define noise packets in freedom outbound that you want to be sent before handshake initiate
3. set noiseKeepAlive: 5 to send noise array every 5 sec (to prevent detection when udp connection getting idle)

in my example it send 4 packets of "ee0000000108aaaa" before handshake

#### it can be used for any UDP configs , not just warp
##### support hex input in Xray>=v25.1.1
##### support noiseKeepAlive and count parameters in Xray>=v25.4.30

<code>noiseKeepAlive: n  ----> send whole noise array every n sec to prevent blockage when udp get idle ( 0==disable_keepalive)
      count: k            ----> send this specific noise k times before moving to next element in array
</code>


#### reference:
https://xtls.github.io/en/config/outbounds/freedom.html#outboundconfigurationobject
