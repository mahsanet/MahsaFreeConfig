### mahsa-xray-core parameters for warp:
<code>
  "mtu": 1280,    
  "wnoise":"ee0000000108aaaa",
  "wnoisecount":"15",
  "wnoisedelay":"1",
  "wpayloadsize":"10",

  "peers": [
    {
      "endpoint": "188.114.98.0:988",
      "keepAlive":  5,
      "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo="
    }
  ],
</code>

### "wnoise"   --->   pattern type to be sent to fool filtering (Default "none")
"" | "none" | "quic" | "random" | any HEX string like "ee0000000108aaaa"<br>
invalid HEX == "none" == "" == absence => (no noise will be send)
### "wnoisecount"   --->   number of noise packets sent (Default "1-2")
"1" | "5" | "1-5" | "10-15" | any number or range (in string format)
### "wnoisedelay"   --->   delay between packets in millisec (Default "5-10")
"1" | "5" | "1-5" | "5-10" | any number or range (in string format)
### "wpayloadsize"   --->   random payload size in byte added to pattern (Default "5-10")
"0" | "1" | "1-5" | "5-10" | any number or range (in string format)
### "keepAlive"   --->   resend noise pattern every n sec (Default 0 )
0 | 1 | 5 | 10 | any number in integer format
0 == disable keepalive (not recommended)<br>
5 == send noise pattern every 5 second(recommended)<br>


### warp key?
get your own warp key using ([Elfiinaa guide](https://github.com/Elfiinaa/ConfigFiles/blob/main/WarpOnWarp.md))<p>

### warp-on-warp?
chain two warp together , hide your country ip , but a bit slower<p>

# caution: 
<b>warp is not hiding your country ip<p>
use it only for normal low-risk activity not trading,banking,...</b>
