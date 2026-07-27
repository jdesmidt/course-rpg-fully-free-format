# Arrays

```
**free

dcl-s  days    varchar(10) dim(7) inz('*');
dcl-s  i       int(10);

days(1) = 'Monday';
days(2) = 'Tuesday';
//...

for i = 1 to 7;
   dsply days(i);
endfor;

for i = 1 to %elem(days);
   dsply days(i);
endfor;

for-each day in days;
  dsply day;
endfor;

for-each day in %list('Saturday' : 'Sunday');
//...
endfor;

sorta days;

sorta(a) days;
sorta(d) days;


*inlr = *on;
```