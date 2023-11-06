# forPracticals

# practical no. 4 Borrower and FINE
plsql-
---------------------------------------------------------

declare
p_roll number;
p_name varchar(50);
p_doi date;
p_nameofbook varchar(50);
p_status char(50);
p_currentDate date;
p_daysLate number;
p_fineAmount number;

begin
p_roll := 3;
p_nameofbook := 'LAB';

select name, doi, status into p_name, p_doi, p_status from borrower where roll = p_roll and nameofbook = p_nameofbook;

p_currentDate := SYSDATE;
p_dayslate:= p_currentDate - p_doi;

if p_daysLate > 30 then
	p_fineAmount := p_daysLate*50;
elsif p_daysLate >=15 then
	p_fineAmount := p_daysLate * 5;
else 
	p_fineAmount := 0;
end if;

if p_fineAmount > 0 then
	insert into fine values (p_roll, p_currentDate, p_fineAmount);
end if;

dbms_output.put_line('Fine Amount: Rs '|| p_fineamount);
commit;

exception
when no_data_found then
	dbms_output.put_line('Borrower of book not found.');
when others then
	dbms_output.put_line('An error occurred');
end;

--------------------------------------------------------------------------
# practical no.  5
--------------------------------------------------------------------------
declare 
r float;
a float;
pi float;

begin 
r:=5;
pi:=3.14;

for r in 9..25 loop
a := pi * (r*r);
dbms_output.put_line('Area of '||r||' is : '|| a);

insert into areaofcircle values (r, a);
end loop;

commit;

end;


...........................................................................
# practical no. 6
---------------------------------------------------------------------------
create or replace procedure proc_grade(
    p_name IN varchar2,
    p_marks IN number,
    p_class out varchar2
) as 
begin 
	if p_marks >=990 and p_marks <= 1500 then
		p_class:= 'Distinction';
	elsif p_marks >=900 and p_marks <=989 then
		p_class:= 'First Class';
	elsif p_marks >=825 and p_marks<=899 then
		p_class:= 'Higher Second Class';
	else
		p_class:= 'Not classified';
	end if;
end;
------------------------------------

declare
name varchar2(50);
marks number;
class varchar2(50);

begin
name :='newStudent';
marks := 1000;

proc_grade(name, marks, class);

dbms_output.put_line(class);
insert into result values(1, name, class);

commit;
end;
--------------------------------------------------------------------------------
I couldn't do 7th practical so its on luck🤞 ☻ 
--------------------------------------------------------
