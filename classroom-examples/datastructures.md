# Data structures

```
**free

dcl-ds t_address template;
    street      varchar(128);
    postcode    varchar(20);
    city        varchar(20);
end-ds;

dcl-ds t_employee template;
    id          int(10);
    name        varchar(50);
    birthplace  varchar(50);
    birthdate   date;
    address     likeds(t_address);
end-ds;

dcl-ds t_employee_multi template;
    id          int(10);
    name        varchar(50);
    birthplace  varchar(50);
    birthdate   date;
    dcl-ds address;
        street      varchar(128);
        postcode    varchar(20);
        city        varchar(20);
    end-ds;
    certificates    varchar(50) dim(10);
end-ds;

dcl-ds employee1    likeds(t_employee_multi);
dcl-ds employee2    likeds(t_employee_multi);
dcl-ds employee3    likeds(t_employee_multi);

dcl-ds employees    likeds(t_employee_multi) dim(999);

employees(1).address.street = '';
employees(1).certificates(5) = 'RPG';

sorta employees(*).name;
sorta employees(*).id;

// id = 5;
employee1.id = 5;

// '20260727'
dcl-ds datefield   len(500);
    dateyear        zoned(4);  // position 1-4
    datemonth       zoned(2); // position 5-6
    dateday         zoned(2); // position 7-8
end-ds;

datefield = '20260801';
dateyear = 2027;
datemonth = 1;
dateday = 1;

dcl-ds datefield;
    dateyearalfa    zoned(4); // position 1-4
    dateyear        char(4) overlay(dateyearalfa); // position 1-4
    datemonth       zoned(2); // position 5-6
    dateday         zoned(2); // position 7-8
end-ds;

dcl-ds datefield;
    dateyearalfa    zoned(4); // position 1-4
    dateyear        char(4) pos(1); // position 1-4
    datemonth       zoned(2); // position 5-6
    dateday         zoned(2); // position 7-8
end-ds;

dcl-ds datefield   qualified;
    dateyear        zoned(4); // position 1-4
    datemonth       zoned(2); // position 5-6
    dateday         zoned(2); // position 7-8
end-ds;


dcl-ds year qualified;
  *n     varchar(11) inz('January');
  *n     varchar(11) inz('February');
  *n     varchar(11) inz('March');
  *n     varchar(11) inz('April');
  *n     varchar(11) inz('May');
  *n     varchar(11) inz('June');
  *n     varchar(11) inz('July');
  *n     varchar(11) inz('August');
  *n     varchar(11) inz('September');
  *n     varchar(11) inz('Oktober');
  *n     varchar(11) inz('November');
  *n     varchar(11) inz('December');
  month  varchar(11) dim(12) pos(1);
end-ds;

dsply year.month(1);  // January

*inlr = *on;
```