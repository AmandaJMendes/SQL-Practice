# SQL-Practice

## Some exercises from https://www.sql-practice.com/  


###### 1) Show first name, last name, and gender of patients who's gender is 'M'
SELECT first_name, last_name, gender  
FROM patients  
WHERE gender = 'M';  

###### 2) Show first name and last name of patients who does not have allergies.
SELECT first_name, last_name  
FROM patients  
WHERE allergies IS NULL;  

###### 3) Show first name of patients that start with the letter 'C'
SELECT first_name  
FROM patients  
WHERE first_name LIKE 'C%';

###### 4) Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
SELECT first_name, last_name  
FROM patients  
WHERE weight between 100 AND 120;

###### 5) Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
UPDATE patients  
SET allergies = 'NKA'  
WHERE allergies is NULL;

###### 6) Show first name and last name concatinated into one column to show their full name.
select first_name || ' ' || last_name  
from patients

###### 7) Show first name, last name, and the full province name of each patient.
select first_name, last_name, province_name  
FROM patients  
INNER JOIN province_names ON province_names.province_id = patients.province_id;

###### 8) Show how many patients have a birth_date with 2010 as the birth year.
SELECT COUNT(*)  
FROM patients  
WHERE YEAR(birth_date) = 2010


###### 9) Show the first_name, last_name, and height of the patient with the greatest height.
SELECT first_name, last_name, MAX(height) as height  
FROM patients;

###### 10) Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000
SELECT *  
FROM patients  
where patient_id in (1,45,534,879,1000);

###### 11) Show the total number of admissions
SELECT COUNT(*)  
from admissions;

###### 12) Show all the columns from admissions where the patient was admitted and discharged on the same day.
SELECT *  
from admissions  
WHERE admission_date = discharge_date;

###### 13) Show the patient id and the total number of admissions for patient_id 579.
SELECT patient_id, count(*) as number_of_admissions  
FROM admissions  
where patient_id = 579;

###### 14) Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?
SELECT distinct city  
FROM patients  
WHERE province_id = 'NS';

###### 15) Write a query to find the first_name, last name and birth date of patients who have height more than 160 and weight more than 70
SELECT first_name, last_name, birth_date  
FROM patients  
where weight > 70 and height > 160;

###### 16) Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null
SELECT first_name, last_name, allergies  
FROM patients  
where city = 'Hamilton' AND allergies is not NULL;

###### 16) Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the result order in ascending by city.
SELECT distinct city  
FROM patients  
where  
city LIKE 'A%' or   
city LIKE 'E%' OR  
city LIKE 'I%' OR  
city LIKE 'O%' OR  
city LIKE 'U%'   
order by city;

###### 18) Show unique birth years from patients and order them by ascending.
SELECT distinct YEAR(birth_date) as birth_year  
FROM patients  
order by birth_year;

###### 19) Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.
SELECT first_name  
FROM patients  
group by first_name  
having count(*) = 1;

###### 20) Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
SELECT patient_id, first_name  
FROM patients  
Where first_name Like 's%s' AND len(first_name) >= 6;

###### 21) Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.
SELECT patients.patient_id, first_name, last_name  
FROM patients  
INNER JOIN admissions ON patients.patient_id = admissions.patient_id  
WHERE admissions.diagnosis = 'Dementia';

###### 22) Display every patient's first_name. Order the list by the length of each name and then by alphbetically
SELECT first_name  
FROM patients  
order by LEN(first_name), first_name;

###### 23) Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.
SELECT  
SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) n_male,  
SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) n_female  
from patients;

###### 24) Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.
SELECT first_name, last_name, allergies  
from patients  
where allergies = 'Penicillin' OR allergies = 'Morphine'  
order by allergies, first_name, last_name;

###### 25) Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.
SELECT patient_id, diagnosis  
FROM admissions  
group by patient_id, diagnosis  
having count(*) > 1;

###### 26) Show the city and the total number of patients in the city.Order from most to least patients and then by city name ascending.
SELECT city, COUNT(*)  
FROM patients  
group by city  
order by count(*) desc, city;

###### 27) Show first name, last name and role of every person that is either patient or doctor. The roles are either "Patient" or "Doctor"
SELECT first_name, last_name, 'Patient' as role  
FROM patients  
UNION ALL  
SELECT first_name, last_name, 'Doctor' as role  
FROM doctors

###### 28) Show all allergies ordered by popularity. Remove NULL values from query.
SELECT allergies, COUNT(*)  
FROM patients  
where allergies IS NOT NULL  
group by allergies  
order by count(*) DESC;

###### 29) Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.
SELECT first_name, last_name, birth_date  
FROM patients  
WHERE YEAR(birth_date) between 1970 AND 1979  
order by birth_date;

###### 30) We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order. EX: SMITH,jane
SELECT UPPER(last_name)|| ',' || Lower(first_name)  
FROM patients  
order by first_name DESC;

###### 31) Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.
SELECT province_id, SUM(height) as total_height  
from patients  
group by province_id  
having total_height >= 7000; 

###### 32) Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'
SELECT MAX(weight) - Min(weight) AS weight_diff  
from patients  
Where last_name = 'Maroni';

###### 33) Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.
SELECT DAY(admission_date), COUNT(*) AS total_adm  
FROM admissions  
group by DAY(admission_date)  
order by total_adm DESC;

###### 34) Show all columns for patient_id 542's most recent admission_date.
SELECT *  
FROM admissions  
WHERE patient_id = 542  
order by admission_date DESC  
LIMIT 1;


###### 35) Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria: 1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19. 2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.
SELECT patient_id, attending_doctor_id, diagnosis  
FROM admissions  
WHERE  
(MOD(patient_id, 2) = 1 AND attending_doctor_id in (1, 5, 19))  
OR  
(CAST(attending_doctor_id AS TEXT) LIKE '%2%' AND  
LEN(CAST(patient_id AS TEXT)) = 3);
 
###### 36) Show first_name, last_name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.
SELECT first_name, last_name, COUNT(*) as total_adm  
FROM admissions  
INNER JOIN doctors ON doctors.doctor_id = admissions.attending_doctor_id  
group by attending_doctor_id;

###### 37) For each doctor, display their id, full name, and the first and last admission date they attended.
SELECT  
doctor_id,  
concat(first_name, ' ', last_name),  
MIN(admission_date),  
MAX(admission_date)

FROM admissions  
INNER JOIN doctors ON doctors.doctor_id = admissions.attending_doctor_id  
group by doctor_id;

###### 38) Display the total amount of patients for each province. Order by descending.
SELECT province_name, COUNT(*) AS province_total  
FROM patients  
INNER JOIN province_names pn ON pn.province_id = patients.province_id  
group by pn.province_id  
order by province_total DESC;

###### 39) For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.
SELECT  
concat(p.first_name, ' ', p.last_name),  
diagnosis,  
CONCAT(d.first_name, ' ', d.last_name)

FROM admissions AS adm  
INNER JOIN doctors AS d ON d.doctor_id = adm.attending_doctor_id  
INNER JOIN patients AS p ON p.patient_id = adm.patient_id;

###### 40) Display the number of duplicate patients based on their first_name and last_name.
SELECT first_name, last_name, COUNT(*) as num_duplicates  
FROM patients  
GROUP by first_name, last_name  
HAVING num_duplicates = 2;

###### 41) Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated. Convert CM to feet by dividing by 30.48. Convert KG to pounds by multiplying by 2.205.
SELECT  
concat(first_name, ' ', last_name),  
ROUND(height / 30.48, 1) as height_feet,  
ROUND(weight * 2.205, 0) AS weight_pound,  
birth_date,  
CASE  
WHEN gender = 'F' THEN 'Female'  
WHEN gender = 'M' Then 'Male'  
END  
FROM patients
