### Normalization Rule for Display

~~~
rule "Primo VE Display- Subject 650"
when
MARC."650" has any "a-z" AND NOT
MARC."650".ind"2" equals "2" AND NOT
MARC."650".ind"2" equals "1"
then
set TEMP"1" to MARC."650" subfields "a-u" delimited by " " remove substring using regex "\\.+$"
set TEMP"2" to MARC."650" sub without sorting "v-z" delimited by " -- "
remove substring using regex (TEMP"2","\\.+$")
concatenate with delimiter (TEMP"1",TEMP"2"," -- ")
set TEMP"3" to multilingual by "650" "Subject" "display"
concatenate with delimiter (TEMP"1",TEMP"3","")
replace string by string (TEMP"1","Indian slaves","Enslaved Indigenous persons")
replace string by string (TEMP"1","Indians of Central America","Indigenous peoples -- Central America")
replace string by string (TEMP"1","Indians of Mexico","Indigenous peoples -- Mexico")
replace string by string (TEMP"1","Indians of North America","Indigenous peoples -- North America")
replace string by string (TEMP"1","Indians of the West Indies","Indigenous peoples -- West Indies")
replace string by string (TEMP"1","Indians of South America","Indigenous peoples -- South America")
        replace string by string (TEMP"1","Eskimos -- Canada, Northern","Inuit -- Canada, Northern")
        replace string by string (TEMP"1","Eskimos -- Greenland","Inuit -- Greenland")
        replace string by string (TEMP"1","Eskimos -- Northwest Territories","Inuit -- Northwest Territories")
        replace string by string (TEMP"1","Eskimos -- Yukon","Inuit -- Yukon")
    replace string by string (TEMP"1","Eskimos -- Canada","Inuit -- Canada") 
     replace string by string (TEMP"1","Eskimos -- Newfoundland","Inuit -- Newfoundland")  
     replace string by string (TEMP"1","Eskimos -- Newfoundland and Labrador","Inuit -- Newfoundland and Labrador")
    replace string by string (TEMP"1","Indian gays","Two-spirit people")       
create pnx."display"."subject" with TEMP"1"
end

~~~
