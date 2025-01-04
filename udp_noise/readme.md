## udp noise

#### introduced 2024-Q4 by @mmmray
 
1. chain udp config outbound to freedom using sockopt
2. define noise packets in freedom that you want to be sent before handshake initiate

in my example it send 4 packets of "ee0000000108aaaa" before handshake

#### it can be used for any UDP configs , not just warp
##### support hex input in Xray>v25.1.1
#### reference:
https://xtls.github.io/en/config/outbounds/freedom.html#outboundconfigurationobject
