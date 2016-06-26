---
title: CSS Trick
layout: post
---

# Horizontal Centering Span that are absolute
once absolutely positioned, it no longer follows the document flow. So the text is centered, but only inside the pink span.  
And since it's absolutely positioned, even if it were a div, the width would collapse.  

```
solution  
span  
{  
    background-color:pink;  
    left: 0;  /*<-*/
    width: 100%;  /*<-*/  
}  
```

> If you don't want the pink to extend the full width, then you must nest an element (e.g. span) inside the positioned spans and give that element the background color, as seen here.
