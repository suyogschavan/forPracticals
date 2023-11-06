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
