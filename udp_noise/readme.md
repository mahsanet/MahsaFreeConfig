## udp noise

#### introduced 2024-Q4 by @mmm
1. first chain udp config outbound to freedom using sockopt
2. define noise packets in freedom that you want to be sent before handshake initiate

in my example it send 5 packets of "ee0000000108aaaa" before handshake

#### it can be used for any UDP configs , not just warp

#### reference:
https://xtls.github.io/en/config/outbounds/freedom.html#outboundconfigurationobject
