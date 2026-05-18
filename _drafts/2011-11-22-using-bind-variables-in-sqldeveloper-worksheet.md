---
title: "Using Bind Variables in SQLDeveloper Worksheet"
date: 2011-11-22
---

In SQL\*Plus, there are two types of variables which  

```
clear screen

variable barry number 

begin
  select 1 into :barry from dual;
end;
/

print barry
```
