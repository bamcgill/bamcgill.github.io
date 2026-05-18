---
title: "Control your SQLcl MCP server database access"
date: 2025-07-21
tags:
  - oracle
  - sqlcl
  - database
  - ai
  - mcp
  - Connections
  - security
---

In [SQLcl 25.2.2](https://download.oracle.com/otn_software/java/sqldeveloper/sqlcl-latest.zip), we introduced a way to point at a specific connection store for use by the MCP server.

We're introducing a new environment variable called DBTOOLS\_HOME which will be used as the connection store for your MCP is defined.

Here, I've configured two mcp servers, one pointing to my  normal local location and one defined with the environment variable DBTOOLS\_HOME pointing at a specific location I want to use to MCP connections

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjMI1X0Fajsv0OdQyCLkoUL2w-Cb40xavjjcoip2iSduMgxcavdvcjgJBcSgvYpLvHbVvWL8dtW_yoOYW5o7IN8DzGlOGEaZt6sYMFAEod6fPPPQqXW9wBa3d512SkWuVHR9b2Xuyb20ohKUdHfPgeoJVnIskja9pN2jjPau4ziYKCSAk155_koOpGYpHg/w382-h198/Screenshot%202025-07-21%20at%2014.43.45.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjMI1X0Fajsv0OdQyCLkoUL2w-Cb40xavjjcoip2iSduMgxcavdvcjgJBcSgvYpLvHbVvWL8dtW_yoOYW5o7IN8DzGlOGEaZt6sYMFAEod6fPPPQqXW9wBa3d512SkWuVHR9b2Xuyb20ohKUdHfPgeoJVnIskja9pN2jjPau4ziYKCSAk155_koOpGYpHg/s603/Screenshot%202025-07-21%20at%2014.43.45.png)

Connecting this to Claude AI, I can see what MCP servers are registered and I can ask Claude what connections it can see in the restricted connection store.  

[![](https://blogger.googleusercontent.com/img/a/AVvXsEhIxzW6PhHw82YYZ4Khg7EAjgyP95sCxEQ2iXLV2NSIMk-KY5F35HhIQuGJRkgMOBgSn_-ylaingqu_j8xrcxG8pBCfKsjxX2lpI0Kr5llZVAf0M6ukhd4bA4r95rV18Ir_z-_roQ9lp8i6iff5oKbz60SUUpZGAKYqM1DjSTBzubye2pwMJ1cGJZagnKU=w394-h172)](https://blogger.googleusercontent.com/img/a/AVvXsEhIxzW6PhHw82YYZ4Khg7EAjgyP95sCxEQ2iXLV2NSIMk-KY5F35HhIQuGJRkgMOBgSn_-ylaingqu_j8xrcxG8pBCfKsjxX2lpI0Kr5llZVAf0M6ukhd4bA4r95rV18Ir_z-_roQ9lp8i6iff5oKbz60SUUpZGAKYqM1DjSTBzubye2pwMJ1cGJZagnKU)

Now, when I ask Claude to list the connections it can see, it returns only one.

  

[![](https://blogger.googleusercontent.com/img/a/AVvXsEjvsTJJPt-yPPmxCNw6Pa1ahPx1_8Rp1AxztuZCW142RwVU9R3sW2NdDEqsdbnNxARobcweCUodX2CofpDK50PbjDSc1xIBTg9_XdROVBnpyJtpM3i9NvryVYVXPId_S2GFE7M93E0AXU68w9pT97iH1s2RCx4hOBDeqypC9dYBTyZrR3DZTdVLL5wJqIE=w411-h200)](https://blogger.googleusercontent.com/img/a/AVvXsEjvsTJJPt-yPPmxCNw6Pa1ahPx1_8Rp1AxztuZCW142RwVU9R3sW2NdDEqsdbnNxARobcweCUodX2CofpDK50PbjDSc1xIBTg9_XdROVBnpyJtpM3i9NvryVYVXPId_S2GFE7M93E0AXU68w9pT97iH1s2RCx4hOBDeqypC9dYBTyZrR3DZTdVLL5wJqIE)

Further, for that connection, we can and should lock the user to only see what you want them to see. like any normal oracle database connection.

create user mcp identified by oracle;

grant connect to mcp;

grant select on hr.employees;

grant select on hr.countries;

grant select on hr.regions;

Finally, we can save the connection to the new connection store by starting SQLcl regularly with the DBTOOLS\_HOME environment variable set.

❯ export DBTOOLS\_HOME=/path/sandbox/mcp/dbtools

❯ sql mcp/oracle@localhost/freepdb1

SQLcl: Release 25.3 Production on Mon Jul 21 14:35:39 2025

Copyright (c) 1982, 2025, Oracle.  All rights reserved.

Connected to:

Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free

Version 23.7.0.25.01

SQL> conn -save min-mcp -savepwd

Name: min-mcp

Connect String: localhost/freepdb1

User: mcp

Password: \*\*\*\*\*\*

SQL>

Now have a least privilege based user created, we can ask Claude to connect to that least privilege connection and tell us what it can see and or do.

[![](https://blogger.googleusercontent.com/img/a/AVvXsEhpMplENY8TKNw4CpndwCSsDQ_MVmI9X2J3EcqWUUOJiZeY3QqbSvFoqh7e3hUJ2fK8RGf4mUGGul0srchQJNXPKzEwd8896k3wAZmGhiAhikW00NYiXLwzf4vanaam7ZMZg1i_UkmwxOQI_0c0f86dmMoTDbUPIPUn9zFExYhir76M3wipIOutRajBQwQ=w630-h876)](https://blogger.googleusercontent.com/img/a/AVvXsEhpMplENY8TKNw4CpndwCSsDQ_MVmI9X2J3EcqWUUOJiZeY3QqbSvFoqh7e3hUJ2fK8RGf4mUGGul0srchQJNXPKzEwd8896k3wAZmGhiAhikW00NYiXLwzf4vanaam7ZMZg1i_UkmwxOQI_0c0f86dmMoTDbUPIPUn9zFExYhir76M3wipIOutRajBQwQ)

  
So, to summarize,  you can control the access you allow the mcp server to have by using standard Oracle database security.  Using the DBTOOLS\_HOME, you can control what connections you allow the MCP server to see and use. [Checkout SQLcl 25.2.2 today](https://www.oracle.com/database/sqldeveloper/technologies/sqlcl/download/)
