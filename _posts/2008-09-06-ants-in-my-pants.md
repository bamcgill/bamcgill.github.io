---
title: "Ants in my pants"
date: 2008-09-06 21:10:00 +0000
last_modified_at: 2008-09-06 21:20:47 +0000
---

Well, just spent the day playing with Ant adding some beanshell scripts and some other bits and pieces.  
  
Here in Oracle, we have the ability to translate to 32 languages pretty quickly given we give our translation teams the appropriate file formats. In SQL Developer, we primarily use three file formats.  

1. property files
2. xliff files ( to denote strings in xml)
3. rts files, home grown strings files we process to java files for inclusion.

Anyway, the upshot of all of this is we are currently going through the pain of translating SQLDeveloper because we are present in close to 100 countries around the globe, even antartica. (Yes guys, we saw you). Translating a tool is an interesting business, both from an operational point of view (how to do it) and when to do it (when in the lifecycle). We'll come to that over time as we solidify this.  
  
Anyway, We've decided that we will drop our first translated delivery with our JDeveloper integration. They normally translate to Japanese, but allows us to work out all the kinks as we go. This will be called our 1.5.2 release and will only be released as part of JDeveloper. As soon as we have that completed, We'll put together 1.5.3 which is a translation of the same tool into 9 languages (including yours hopefully)
