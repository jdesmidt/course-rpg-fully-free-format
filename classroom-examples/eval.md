# Eval statements

```
**Free


dcl-s   field   char(5);            // '_____'

field = 'ABC';                      // 'ABC__';
eval field = 'ABC';                 // 'ABC__';

evalr field = 'ABC';                // '__ABC';


*inlr = *on;
```