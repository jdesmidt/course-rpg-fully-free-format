# Selections and iterations

```
**free

dcl-s i    int(10);

if ( companyid = 'AB');
// ...
endif;

if ( companyid = 'AB');
// ...
else;
// ...
endif;

if ( companyid = 'AB');
// ...
elseif ( companyid = 'CD');
// ...
elseif ( companyid = 'EF');
// ...
else;
// ...
endif;

select;
when companyid = 'AB';
// ..
when companyid = 'CD';
// ..
other;
// ..
endsl;

for i = 1 to 10;
// ...
endfor;

for i = 10 downto 1;
// ...
endfor;

// do while
dow (i < 10);
    i += 1;
enddo;

// do until
dou (i < 10);
    i += 1;
enddo;

clear x;

x = 0;

dow 1=1;
    if (x = 3);
        x = 4;
        iter;
    endif;

    if (x > 5);
        leave;
    endif;

    x += 1;
enddo;

*inlr = *on;
```