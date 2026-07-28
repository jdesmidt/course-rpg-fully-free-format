
```
**free

dcl-s    year     char(4);

dcl-s    datefield  date(*iso);
dcl-s    leapyear   ind;


// -------------------------------------------------------------
//  MAIN
// -------------------------------------------------------------
year = '2026';
exsr isleapyear;

year = '2028';
exsr isleapyear;

year = '2030';
exsr isleapyear;

*inlr = *on;

// -------------------------------------------------------------
//  check if leapyear
// -------------------------------------------------------------
begsr   isleapyear;

datefield = %date(year + '-01-01');

datefield = datefield + %months(2);
datefield = datefield - %days(1);

if %subdt( datefield : *days ) = 29;
  leapyear = *on;
  dsply ( year + ' is a leapyear');
else;
  leapyear = *off;
  dsply ( year + ' is not a leapyear');
endif;

endsr;

```
