---
title: "Continuous Integration for SQL Tasks"
date: 2012-04-10 21:04:00 +0000
last_modified_at: 2012-04-10 21:04:46 +0000
tags:
  - Oracle Develop
  - image
  - continuous integration
  - virtualbox
  - linux
  - Hudson
---

One of my favourite integration tools is [hudson](http://hudson-ci.org/).   Today, we're going to show you how to setup hudson on the [Oracle Developer Day image](http://www.oracle.com/technetwork/community/developer-vm/index.html).  Since the image is built on Enterprise Linux, we'll need to either add a yum repository from which to install, or, even easier, just download the RPM from the hudson site  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEho7ISuZHdgVAYo_67disU7rxsbYwEHGPQGq3aciwOGn2e0npJcYdNHsLdHluc72PNr6CwyOn1ctBDa8-A0Bcb6v8O4D7zXci-bSbGy8a5Q3071wcuE6FNBSAjZ45MYwSrx7yf4ury3AA0/s1600/Screen+Shot+2012-04-10+at+21.05.09.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEho7ISuZHdgVAYo_67disU7rxsbYwEHGPQGq3aciwOGn2e0npJcYdNHsLdHluc72PNr6CwyOn1ctBDa8-A0Bcb6v8O4D7zXci-bSbGy8a5Q3071wcuE6FNBSAjZ45MYwSrx7yf4ury3AA0/s1600/Screen+Shot+2012-04-10+at+21.05.09.png)

Clicking on the Oracle Linux link, we'll download hudson-redhat-2.2.0.rpm.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeXBIvqQzsOA8ypbqI8AbWaxMLDByn1KU6hqbkfAt0SLFleh6f4RLE3qINdgs_ePTB6AzWRPwhF74MwDLSZ_wK-UXyDV0_C-N7SP8lWRcv1uXZL1egX6rBEIF3K6_fx1mRZ_DESAa5QIQ/s1600/Screen+Shot+2012-04-10+at+21.07.54.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeXBIvqQzsOA8ypbqI8AbWaxMLDByn1KU6hqbkfAt0SLFleh6f4RLE3qINdgs_ePTB6AzWRPwhF74MwDLSZ_wK-UXyDV0_C-N7SP8lWRcv1uXZL1egX6rBEIF3K6_fx1mRZ_DESAa5QIQ/s1600/Screen+Shot+2012-04-10+at+21.07.54.png)

When its downloaded, you can install it on your linux image.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZDfAwIBFn9P31Sh8FGuiqKC5efLhsKxqIf4UxxlWX5j5UbJFylx4dTSTaamadw7CsinmoZYE5KquZ8-Mhq-09GL3VZeDhkVfCA5O0VruVi94vyuYrKJ35hMjREotujRGcByyxTjVXNBc/s400/Screen+Shot+2012-04-10+at+21.12.16.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZDfAwIBFn9P31Sh8FGuiqKC5efLhsKxqIf4UxxlWX5j5UbJFylx4dTSTaamadw7CsinmoZYE5KquZ8-Mhq-09GL3VZeDhkVfCA5O0VruVi94vyuYrKJ35hMjREotujRGcByyxTjVXNBc/s1600/Screen+Shot+2012-04-10+at+21.12.16.png)

Now, its installed, we need to configure it.  Since we put in the RPM, there are a couple of standard directories to check.  Firstly, we have an init.d script for starting and stopping hudson  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhnvZORDzoqd6j4QTg0q5xyFaoP13aYACI6yLdGLcPVqcwbdIz5qbT3XhQ_zO3e-wBGLNfyc3USAJC1XA8ysKZuTvfNmTqJATAA_J5z6WODqVMNDA9qSWHrx6JfNv3kh4XCL5DWubHACaU/s320/Screen+Shot+2012-04-10+at+21.20.36.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhnvZORDzoqd6j4QTg0q5xyFaoP13aYACI6yLdGLcPVqcwbdIz5qbT3XhQ_zO3e-wBGLNfyc3USAJC1XA8ysKZuTvfNmTqJATAA_J5z6WODqVMNDA9qSWHrx6JfNv3kh4XCL5DWubHACaU/s1600/Screen+Shot+2012-04-10+at+21.20.36.png)

So, to configure hudson, the actual configuration file is under /etc/sysconfig.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhj0im07I_dl2w4pBdyjTrfX2c6Uvz1iiDr-8uXbjHOnpOTKhCiJR7tAiYcf9tV0RMDlJcSGHvvd8-cRbPQqanBW-NiXm2pjIEb-Ki9lwqslbljowGMtXW66NQK47dcsmkFfV9G1hcZJ84/s320/Screen+Shot+2012-04-10+at+21.21.35.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhj0im07I_dl2w4pBdyjTrfX2c6Uvz1iiDr-8uXbjHOnpOTKhCiJR7tAiYcf9tV0RMDlJcSGHvvd8-cRbPQqanBW-NiXm2pjIEb-Ki9lwqslbljowGMtXW66NQK47dcsmkFfV9G1hcZJ84/s1600/Screen+Shot+2012-04-10+at+21.21.35.png)

At this point, the main thing we want to do is to configure the port that hudson will operate on.  We'll change ours to 8888, since the image has several other ports doing different things.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFEU57YVGACErHY2wAgA_QfEYqNSmsebLzvpS8X7cRJXSd6YGSqMi4_CeuArO0crhuFU2LJPewla896rmqo9N5r99nP3b0sq6OWlLMaeZO9ol3nSnRj0UJNnnQb8puhv3fEUe1WtARz58/s320/Screen+Shot+2012-04-10+at+21.24.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFEU57YVGACErHY2wAgA_QfEYqNSmsebLzvpS8X7cRJXSd6YGSqMi4_CeuArO0crhuFU2LJPewla896rmqo9N5r99nP3b0sq6OWlLMaeZO9ol3nSnRj0UJNnnQb8puhv3fEUe1WtARz58/s1600/Screen+Shot+2012-04-10+at+21.24.45.png)

Now, once thats done, come back to /etc/init.d and run hudson start.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiB8KjlbfrbLdHPb-ZsqeyVv6yBPgeNCFGozKd-IU7XfxB9G1rwqgleb93KBYFes95SnIk8bhSVJ57GCvRu0y94gLE6DaiFffFpLz_YBl9OCS60njjTTq6oI_rch1Q4TQ75XzYvQ02ActE/s320/Screen+Shot+2012-04-10+at+21.32.06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiB8KjlbfrbLdHPb-ZsqeyVv6yBPgeNCFGozKd-IU7XfxB9G1rwqgleb93KBYFes95SnIk8bhSVJ57GCvRu0y94gLE6DaiFffFpLz_YBl9OCS60njjTTq6oI_rch1Q4TQ75XzYvQ02ActE/s1600/Screen+Shot+2012-04-10+at+21.32.06.png)

  
  
So now, fireup firefox on the image and punch in localhost:8888  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigiKVEhtOHIGC2TimJ34PrYtw3_M6lA9L14N2ep-4JC7yFeCCHNut9ndGGe1KtEAY9o0C8wqVI3yw8P3vU5rHB7F0JwUoFK4X5R9RPx9c492E3U8S7d1H5tYTbhtOtE6l4fnMspCe5L4g/s320/Screen+Shot+2012-04-10+at+21.32.35.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigiKVEhtOHIGC2TimJ34PrYtw3_M6lA9L14N2ep-4JC7yFeCCHNut9ndGGe1KtEAY9o0C8wqVI3yw8P3vU5rHB7F0JwUoFK4X5R9RPx9c492E3U8S7d1H5tYTbhtOtE6l4fnMspCe5L4g/s1600/Screen+Shot+2012-04-10+at+21.32.35.png)

  
  
Which will give us this.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXiYD29R8LBFJ04TwiZiMVNOfe9U2ukFatoJMTFsCNdh2jb_NRfgkhf5n3eG6XE-QMHZc9Z6PGJ5vKk9ID5VOob8pMeUdHkUbPQR7pAffnUhkMMZPQz6PwztcydDy77tnDzqjsQfDR8gM/s320/Screen+Shot+2012-04-10+at+21.34.18.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXiYD29R8LBFJ04TwiZiMVNOfe9U2ukFatoJMTFsCNdh2jb_NRfgkhf5n3eG6XE-QMHZc9Z6PGJ5vKk9ID5VOob8pMeUdHkUbPQR7pAffnUhkMMZPQz6PwztcydDy77tnDzqjsQfDR8gM/s1600/Screen+Shot+2012-04-10+at+21.34.18.png)

  
  
 Tada!.  now we have hudson up and running.  Lets run a dumb job to see what happens,  I'll do something really simple so you can try this immediately.  

```
ls -altr
touch barry.txt
echo "Something $BUILD_NUMBER" >> barry.txt
cat barry.txt
```

  
  
creating a new job on hudson is easy.  Click on the new job icon and enter the name and description of your job.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhb68L2_XSAY1c_jEnqEewmg8nFNn2twDJkGNlx5Yav_uvmFfU4Zbm0UD6BSYeL3zFzUBRlyH4F0Fid23ughBEp_wouHi5DW5bNoonlyWzMQ-jqCKtTEc6J2HkTiaGpqBdumxC5St1V_Uk/s320/Screen+Shot+2012-04-10+at+21.40.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhb68L2_XSAY1c_jEnqEewmg8nFNn2twDJkGNlx5Yav_uvmFfU4Zbm0UD6BSYeL3zFzUBRlyH4F0Fid23ughBEp_wouHi5DW5bNoonlyWzMQ-jqCKtTEc6J2HkTiaGpqBdumxC5St1V_Uk/s1600/Screen+Shot+2012-04-10+at+21.40.45.png)

  
  
Scroll down and choose a build option of Shell script.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgq8lkNNqQWOolb9W3kxKyBHczjH68QYjNWNKO47OEF6h1AXrakNbFmct4ArDlI1wpzYkZ6UuRGCOakEl4x4wprUU5cfbk0jVwvu0Dkl5joKSn5ULNNt_vHCv-sPnAe9qEcIO7fUOgzNU/s1600/Screen+Shot+2012-04-10+at+21.42.52.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhgq8lkNNqQWOolb9W3kxKyBHczjH68QYjNWNKO47OEF6h1AXrakNbFmct4ArDlI1wpzYkZ6UuRGCOakEl4x4wprUU5cfbk0jVwvu0Dkl5joKSn5ULNNt_vHCv-sPnAe9qEcIO7fUOgzNU/s1600/Screen+Shot+2012-04-10+at+21.42.52.png)

And now add our little script.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjM484nAz3DflEANAw8yE0TTBDKbHl_f2zqQ-5HfIoKYML-e2vpsLuJs7J7cwafPSre6Y4juggqAR-KBZyOP2B7ZatZUF66TrrD-zz5_kMw1v5F1tiJr3AAySYp3IvrvCBtx_pANvvv60E/s320/Screen+Shot+2012-04-10+at+21.44.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjM484nAz3DflEANAw8yE0TTBDKbHl_f2zqQ-5HfIoKYML-e2vpsLuJs7J7cwafPSre6Y4juggqAR-KBZyOP2B7ZatZUF66TrrD-zz5_kMw1v5F1tiJr3AAySYp3IvrvCBtx_pANvvv60E/s1600/Screen+Shot+2012-04-10+at+21.44.45.png)

  
  
and click save at the bottom.  Job done, so to speak.  
Now run the job and see what happens.  It will queue it up and run it and when its finished, will show an icon as to whether there is thunder coming or the sun is still shining.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTq57gxmOK1B7mDL426Tbxd6TSOvW8YHNkf32bo2crXxN7X_FWG_XgJdiyUsE7Ihb9cDWuQvuW2RooKRD7kvvMy4iRPtRkNZ6OM_VO2XlAAwHjR1sgjYTuxSRngoMyspBRNZsfAV-hKuE/s320/Screen+Shot+2012-04-10+at+21.47.38.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTq57gxmOK1B7mDL426Tbxd6TSOvW8YHNkf32bo2crXxN7X_FWG_XgJdiyUsE7Ihb9cDWuQvuW2RooKRD7kvvMy4iRPtRkNZ6OM_VO2XlAAwHjR1sgjYTuxSRngoMyspBRNZsfAV-hKuE/s1600/Screen+Shot+2012-04-10+at+21.47.38.png)

Drilling into the job, you can click on the console output to see how the job actually ran.    

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiC6LhVzPvS8NgTMqTAk0TYNwsssdlWa-kAe6VzG_ZRT24CTRDcKVyqGPLOYcRZYh4hxCgbv3fiqPUePnBST5NmJO7DHvzaYgZGEqGJAt_4ZwzVUa8UcByqJtPSHq8vZ9lp0qPBTWUwS4Q/s320/Screen+Shot+2012-04-10+at+21.48.14.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiC6LhVzPvS8NgTMqTAk0TYNwsssdlWa-kAe6VzG_ZRT24CTRDcKVyqGPLOYcRZYh4hxCgbv3fiqPUePnBST5NmJO7DHvzaYgZGEqGJAt_4ZwzVUa8UcByqJtPSHq8vZ9lp0qPBTWUwS4Q/s1600/Screen+Shot+2012-04-10+at+21.48.14.png)

There it is running.  One last step.  We need to add a port forwarding rule to the image so we can check this out from outside the image. and we're done.   

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9ifmDTKMa8LLwUDZ3_2IxeY0anHR0x9Fyc3UsdezDk8yq-NorTsnxexUfqh3NjbXeSbFkX_tfLfKPoUnYzFn2m31fOPPixmaazgPpebDIEj_jWUmmY_YZJVcYAzI0YJWdSobepW6z9qE/s320/Screen+Shot+2012-04-10+at+22.03.21.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9ifmDTKMa8LLwUDZ3_2IxeY0anHR0x9Fyc3UsdezDk8yq-NorTsnxexUfqh3NjbXeSbFkX_tfLfKPoUnYzFn2m31fOPPixmaazgPpebDIEj_jWUmmY_YZJVcYAzI0YJWdSobepW6z9qE/s1600/Screen+Shot+2012-04-10+at+22.03.21.png)

  
  
 I've just noticed too, that apex seems to be configured with port 8888, so we could get a clash later.  I will change that on this image.  Anyways, have fun with this for now.  I'll come back to this when we get subversion setup and linked to this so we can checkout the sql/plsql and run tests using this hudson install.
