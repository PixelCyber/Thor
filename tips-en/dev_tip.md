## Thor Debug & Analyze Tips


### Sniffer tips

* Turn off local proxy to ignore local device traffic, when you sniff other device.

* Use a session filter to ignore non-target traffic and improve sniffer performance.

* Use a packet filter to query target records only.


### Develop & Debug tips

* Set HTTP proxy with Thor proxy address like `127.0.0.1:8423` in your source code to debug traffic.

* Set a keyword field in HTTP Head to identify requests, then filter this keyword with `Session Filter` in Thor.

