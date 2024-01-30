# Summer-of-SQL
## Solution

  SELECT 
    * 
  FROM 
    crime_scene_report 
  where 
    date = '20180115' 
    and city = 'SQL City';


  SELECT 
    * 
  from 
    person 
  where 
    address_street_name = 'Northwestern Dr' 
  order by 
    address_number DEsc 
  limit 
    1;

id	name	license_id	address_number	address_street_name	ssn
14887	Morty Schapiro	118009	4919	Northwestern Dr	111564949

 
SELECT *
from person
where address_street_name = 'Franklin Ave'
and name like 'Annabel%'; 




SELECT 
  * 
from 
  person 
where 
  address_street_name = 'Franklin Ave' 
  and name like 'Annabel%';


SELECT 
  * 
from 
  person as p 
  join drivers_license as dl on dl.id = p.license_id 
  join get_fit_now_member as gfnm on p.id = gfnm.person_id 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  plate_number like '%H42W%';



SELECT 
  * 
from 
  get_fit_now_member as gfnm 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  person_id = 16371;

SELECT 
  * 
from 
  get_fit_now_check_in as gfnci 
where 
  check_in_time between 1600 
  and 1700;


SELECT 
  * 
from 
  get_fit_now_member as gfnm 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  membership_id = '48Z7A' 
  or membership_id = '90081';



value
Congrats, you found the murderer! But wait, there's more... If you think you're up for a challenge, try querying the interview transcript of the murderer to find the real villain behind this crime. If you feel especially confident in your SQL skills, try to complete this final step with no more than 2 queries. Use this same INSERT statement with your new suspect to check your answer.


SELECT 
  * 
from 
  interview 
where 
  person_id = 67318;



select 
  * 
from 
  person as p 
  join drivers_license as dl on p.license_id = dl.id 
  join facebook_event_checkin as fb on p.id = fb.person_id 
where 
  car_make = 'Tesla' 
  and height between 65 
  and 67;

              
id	name	license_id	address_number	address_street_name	ssn	id	age	height	eye_color	hair_color	gender	plate_number	car_make	car_model	person_id	event_id	event_name	date
13064	Dion Montague	467669	485	Briggs Blvd	184082532	467669	70	65	green	white	male	W528W7	Tesla	Model S	13064	8753	three friends. If they're ok, you're it.	20170110
99716	Miranda Priestly	202298	1883	Golden Ave	987756388	202298	68	66	green	red	female	500123	Tesla	Model S	99716	1143	SQL Symphony Concert	20171206
99716	Miranda Priestly	202298	1883	Golden Ave	987756388	202298	68	66	green	red	female	500123	Tesla	Model S	99716	1143	SQL Symphony Concert	20171212
99716	Miranda Priestly	202298	1883	Golden Ave	987756388	202298	68	66	green	red	female	500123	Tesla	Model S	99716	1143	SQL Symphony Concert	20171229
