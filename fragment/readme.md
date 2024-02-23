### convert your config link into fragment json using this tool:<p>
https://ircfspace.github.io/fragment/<p>
https://ircf.space/<p><p><p>



### if you are using [our new xray-core](https://github.com/GFW-knocker/Xray-core/releases/latest/):<p>
you can use <code>fakehost</code> option in fragment for http or ws config<p>
recommended setting for noTLS (80,8080,2052,2082,2086,2095):
<code>
"packets": "fakehost",
"length": "10-20",
"interval": "10-20",
"host1_domain":"cloudflare.com",  
"host2_domain":"cloudflare.com"
</code>
<p></p>
recommended setting for TLS (443,8443,2053,2083,2087,2096):
<code>
"packets": "tlshello",
"length": "10-20",
"interval": "10-20"
</code>
