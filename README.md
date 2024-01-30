# Summer-of-SQL


Solution

Jan.15, 2018 and that it took place in SQL City.

  SELECT 
    * 
  FROM 
    crime_scene_report 
  where 
    date = '20180115' 
    and city = 'SQL City';


date	type	description	city
20180115	assault	Hamilton: Lee, do you yield? Burr: You shot him in the side! Yes he yields!	SQL City
20180115	assault	Report Not Found	SQL City
20180115	murder	Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".	SQL City


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

id	name	license_id	address_number	address_street_name	ssn
16371	Annabel Miller	490173	103	Franklin Ave	318771143



SELECT 
  * 
from 
  person 
where 
  address_street_name = 'Franklin Ave' 
  and name like 'Annabel%';

person_id	transcript
14887	I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".
16371	I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.


SELECT 
  * 
from 
  person as p 
  join drivers_license as dl on dl.id = p.license_id 
  join get_fit_now_member as gfnm on p.id = gfnm.person_id 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  plate_number like '%H42W%';

id	name	license_id	address_number	address_street_name	ssn	id	age	height	eye_color	hair_color	gender	plate_number	car_make	car_model	id	person_id	name	membership_start_date	membership_status
67318	Jeremy Bowers	423327	530	Washington Pl, Apt 3A	871539279	423327	30	70	brown	brown	male	0H42W2	Chevrolet	Spark LS	48Z55	67318	Jeremy Bowers	20160101	gold



SELECT 
  * 
from 
  get_fit_now_member as gfnm 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  person_id = 16371;

id	person_id	name	membership_start_date	membership_status	membership_id	check_in_date	check_in_time	check_out_time
90081	16371	Annabel Miller	20160208	gold	90081	20180109	1600	1700


SELECT 
  * 
from 
  get_fit_now_check_in as gfnci 
where 
  check_in_time between 1600 
  and 1700;
	
membership_id	check_in_date	check_in_time	check_out_time
48Z7A	20180109	1600	1730
90081	20180109	1600	1700


SELECT 
  * 
from 
  get_fit_now_member as gfnm 
  join get_fit_now_check_in as gfnci on gfnm.id = gfnci.membership_id 
where 
  membership_id = '48Z7A' 
  or membership_id = '90081';

id	person_id	name	membership_start_date	membership_status	membership_id	check_in_date	check_in_time	check_out_time
48Z7A	28819	Joe Germuska	20160305	gold	48Z7A	20180109	1600	1730
90081	16371	Annabel Miller	20160208	gold	90081	20180109	1600	1700



value
Congrats, you found the murderer! But wait, there's more... If you think you're up for a challenge, try querying the interview transcript of the murderer to find the real villain behind this crime. If you feel especially confident in your SQL skills, try to complete this final step with no more than 2 queries. Use this same INSERT statement with your new suspect to check your answer.


SELECT 
  * 
from 
  interview 
where 
  person_id = 67318;

person_id	transcript
67318	I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017.


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
