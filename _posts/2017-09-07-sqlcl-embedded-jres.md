---
title: "SQLcl Embedded JREs"
date: 2017-09-07 10:09:00 +0000
last_modified_at: 2017-09-07 10:09:28 +0000
tags:
  - jre
  - embedded
  - sqlcl
---

When you are restrained in the JRE that you can use with SQLcl, you can embed your own in the sqlcl directory tree.  We currently support 1.8 meaning that if you run with 1.7, you're going to have problems.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6RarTMUYsz9aWzxqPTocj5-P47pggDaaCZHJFVcOmDwpa8KUXWDZHv-hyCUwyRqOJgeUd14UCfAa4pXaXanbnsvqduvmao2Nk-XM5zIjZ5RVmYmDDIp-i_KBUIHNuqYfOZwvsv5n1sE0/s320/Screen+Shot+2017-09-07+at+10.52.19.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6RarTMUYsz9aWzxqPTocj5-P47pggDaaCZHJFVcOmDwpa8KUXWDZHv-hyCUwyRqOJgeUd14UCfAa4pXaXanbnsvqduvmao2Nk-XM5zIjZ5RVmYmDDIp-i_KBUIHNuqYfOZwvsv5n1sE0/s1600/Screen+Shot+2017-09-07+at+10.52.19.png)

When you look inside a sqlcl distribution, you will see the bin and lib directory.

Go grab a jre from somewhere, In my case, I'm getting it from my installed jdk

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiGOUg_R58cNgblLFIqNHgYAuG5uVNIlr2RhaEh2GVWTHmRrCxUBzSOR-kLolLYyY2z6TCx0NG_JSdaR5ImpuFOV4s3iKW7XV5cw8i_mEmL-fRmELJ3-kSnKYHEwTUhcm7MjIrUjCmBPyo/s320/Screen+Shot+2017-09-07+at+10.54.57.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiGOUg_R58cNgblLFIqNHgYAuG5uVNIlr2RhaEh2GVWTHmRrCxUBzSOR-kLolLYyY2z6TCx0NG_JSdaR5ImpuFOV4s3iKW7XV5cw8i_mEmL-fRmELJ3-kSnKYHEwTUhcm7MjIrUjCmBPyo/s1600/Screen+Shot+2017-09-07+at+10.54.57.png)

Zip up the JRE and unzip it in the top level sqlcl directory.  You should have a structure like this now.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgNjqj45sUan6wiJURosdrMog4VVIPXFG7Uro3SpdcqGENMnBpXvsIuuLb3GA_Hvw-75yoD4tL2pWL9UdkaG_CjSQ82uAX1whZNSnXRGLolaRDXnTgXifi3bKkj7i5MpFyk6C_WK8AzE84/s320/Screen+Shot+2017-09-07+at+10.57.40.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgNjqj45sUan6wiJURosdrMog4VVIPXFG7Uro3SpdcqGENMnBpXvsIuuLb3GA_Hvw-75yoD4tL2pWL9UdkaG_CjSQ82uAX1whZNSnXRGLolaRDXnTgXifi3bKkj7i5MpFyk6C_WK8AzE84/s1600/Screen+Shot+2017-09-07+at+10.57.40.png)

Test what you have now by running SQLcl.  I'm doing a silent run to test it works for a start and also to check where the java is coming from. If you type 'show java' you'll get a lot of information about what is running and where it is.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhl2RKWavxrMPFQrINNTiQ1BxG06IBKVWUHb1X0feVnKOtkMW47cGPrnkHHyPmepDwrRNluValHWbPwTS6pOZkK2g0S3feBZr_6JOrKafumDk6QwDeuletEZSKTCFvrVfQldpQoxf7gceQ/s320/Screen+Shot+2017-09-07+at+10.58.40.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhl2RKWavxrMPFQrINNTiQ1BxG06IBKVWUHb1X0feVnKOtkMW47cGPrnkHHyPmepDwrRNluValHWbPwTS6pOZkK2g0S3feBZr_6JOrKafumDk6QwDeuletEZSKTCFvrVfQldpQoxf7gceQ/s1600/Screen+Shot+2017-09-07+at+10.58.40.png)

You can see here that the JRE from the installtion is being used so you can now drop this in another environment and run normally.
