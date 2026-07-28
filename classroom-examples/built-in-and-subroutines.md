```

**free

ctl-opt    text('Review') copyright('me');
ctl-opt    decedit('0.');

dcl-s    num1   packed(12);
dcl-s    num2   zoned(5);
dcl-s    num3   int(10);    // int(3)  int(5)  int(10) int(20)
dcl-s    num4   zoned(7:2);

dcl-s    char1  char(50);
dcl-s    char2  varchar(128);
dcl-s    succes ind;

dcl-s    pcustomer   pointer;

dcl-s    today       date(*dmy/);
dcl-s    datefield_eur   date(*eur);
dcl-s    now         time;
dcl-s    now2        timestamp(*iso:0);

dcl-s    months      char(10) dim(12);

dcl-ds   t_address     qualified template;
    street         char(100);
    nr             int(10);
end-ds;

dcl-s   workaddress    likeds(t_address);
dcl-s   prefix         char(2);
dcl-s   text1          char(50) inz('    Amsterdam   ');

dcl-s   pos            int(10);
dcl-s   len            int(10);

dcl-s   dummy          varchar(100);

workaddress.street = 'This Street';

num = 5;

prefix = %subst( workaddress.street : 1 : 2);   // Th
prefix = %subst( workaddress.street : 1 : 2);   // Th
prefix = %subst( workaddress.street : 6 );      // Street

dummy = %trim( text1 );
dummy = %trimr( text1 );
dummy = %triml( text1 );


pos = %scan( 'A' : text1 );  

dummy = %replace( 'Rotter' : text1 : 5 : 10 );

len = %len( text1 );
len = %len( %trim( text1 ));

dummy = %scanrpl(' ' : '_' : text1 );
dummy = %scanrpl('ABC' : 'X' : text1 );

dummy = %lower( text1 );
dummy = %upper( text1 );

dummy = '14.125';
num4 = %dec( dummy );

dummy = 'ABCD';
num4 = %dec( dummy );   // MSGW

num3 = %int( '000000015' );   // 15

dummy = %char( num4 ); 

today = %date('2026-07-28');
today = %date();

datefield_eur = today;
datefield_eur = today + %months(1) + %days(10);

now = %time();
now = %time() + %minutes(1) - %hours(12);

now2 = %timestamp();

// dcl-s    months      char(10) dim(12) inz('');

months = %list('January' : 'February' : 'March' : ...);

num = %elem(months);

for i = 1 to %elem(months);
endfor;

// dcl-s values     int(10) dim(100);
// dcl-s values10   int(10) dim(100);
num = %max(values);
num = %min(values);
values10 = %subarr( values : 1 : 10);

num = %lookup( 'June' : months );

// dcl-s  months   char(3) dim(6);
text = 'Jan;Feb;Mrt;Apr;May;Jun';
months = %split( text : ';');


// Subroutines 1
// -------------
// dcl-s total    zoned(12);
// dcl-s amount   zoned(12);

total = 0;

amount = 10;
//total += amount;
exsr AddToTotal;

amount = 20;
//total += amount;
exsr AddToTotal;

amount = 15;
//total += amount;
exsr AddToTotal;

begsr AddToTotal;

   total += amount;
endsr;

// Subroutines 2
// -------------
exsr  ReadEmployee;

dow  employee_found:
    exsr  ProcessEmployee;
    exsr  ReadEmployee;
enddo;

begsr ReadEmployee;
   // read file
   employee_found = *on;
endsr;

begsr ProcessEmployee;
    if (employeetype = 'xx');
        leavesr;    // leaves the subroutine
    endif;
    // ...
endsr;

dow 1=1;
    exsr  ReadEmployee;
    if (not employee_found);
        leave;
    endif;
    exsr  ProcessEmployee;
enddo;


*inlr = *on;


exsr $$endpgm;

// Initialisation subroutine
begsr *inzsr;
   today = %date();
endsr;

begsr  $$endpgm;
    *inlr = *on;
    return;
endsr;
```
