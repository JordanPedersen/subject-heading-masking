# Bibliographic Normalization Rules
There are 3 normalization rules that get strung together to make the normalization process.

## Rule 1 adds the new 650 field
Note: it was not working for subfields that end in a period. Case opened with ExLibris # 06404456

~~~
Rule 1
rule "Indigenous SH - Enslaved Indigenous persons"
when
((exists "650.a.Indian slaves") and (not exists "650.a.Enslaved Indigenous persons"))
then
addField "650.{-,7}.a.Enslaved Indigenous persons"
end
 
rule "Indigenous SH - Enslaved Indigenous persons - fast"
when
((exists "650.a.Indian slaves\\\\.") and (not exists "653.a.Enslaved Indigenous persons"))
then
addField "650.{-,7}.a.Enslaved Indigenous persons"
end
 
rule "Indigenous SH - Inuit -- Canada, Northern"
when
((exists "650.a.Eskimos") and (exists "650.z.Canada, Northern"))
then
addField "650.{-,7}.a.Inuit -- Canada, Northern"
end
 
rule "Indigenous SH - Inuit -- Greenland"
when
((exists "650.a.Eskimos") and (exists "650.z.Greenland"))
then
addField "650.{-,7}.a.Inuit -- Greenland"
end
 
rule "Indigenous SH - Inuit -- Northwest Territories"
when
((exists "650.a.Eskimos") and (exists "650.z.Northwest Territories"))
then
addField "650.{-,7}.a.Inuit -- Northwest Territories"
end
 
rule "Indigenous SH - Inuit -- Yukon"
when
((exists "650.a.Eskimos") and (exists "650.z.Yukon"))
then
addField "650.{-,7}.a.Inuit -- Yukon"
end

rule "Indigenous SH - Inuit -- Canada"
when
((exists "650.a.Eskimos") and (exists "650.z.Canada"))
then
addField "650.{-,7}.a.Inuit -- Canada"
end

rule "Indigenous SH - Inuit -- Newfoundland"
when
((exists "650.a.Eskimos") and (exists "650.z.Newfoundland"))
then
addField "650.{-,7}.a.Inuit -- Newfoundland"
end

rule "Indigenous SH - Inuit -- Newfoundland and Labrador"
when
((exists "650.a.Eskimos") and (exists "650.z.Newfoundland and Labrador"))
then
addField "650.{-,7}.a.Inuit -- Newfoundland and Labrador"
end

rule "Indigenous SH - Indigenous Peoples Central America"
when
(exists "650.a.Indians of Central America")
then
addField "650.a.Indigenous peoples -- Central America"
end

rule "Indigenous SH - Indigenous Peoples Central America - fast"
when
(exists "650.a.Indians of Central America\\\\.")
then
addField "650.a.Indigenous peoples -- Central America"
end

rule "Indigenous SH - Indigenous Peoples North America"
when
(exists "650.a.Indians of North America")
then
addField "650.a.Indigenous peoples -- North America"
end

rule "Indigenous SH - Indigenous Peoples North America - fast"
when
(exists "650.a.Indians of North America\\\\.")
then
addField "650.a.Indigenous peoples -- North America"
end

rule "Indigenous SH - Indigenous Peoples South America"
when 
(exists "650.a.Indians of South America")
then
addField "650.a.Indigenous peoples -- South America"
end

rule "Indigenous SH - Indigenous Peoples South America - fast"
when 
(exists "650.a.Indians of South America\\\\.")
then
addField "650.a.Indigenous peoples -- South America"
end

rule "Indigenous SH - Indigenous Peoples of the West Indies"
when
(exists "650.a.Indians of the West Indies")
then
addField "650.a.Indigenous peoples -- West Indies"
end

rule "Indigenous SH - Indigenous Peoples of the West Indies - fast"
when
(exists "650.a.Indians of the West Indies\\\\.")
then
addField "650.a.Indigenous peoples -- West Indies"
end

rule "Indigenous SH - Indigenous Peoples Mexico"
when
(exists "650.a.Indians of Mexico")
then
addField "650.a.Indigenous peoples -- Mexico"
end

rule "Indigenous SH - Indigenous Peoples Mexico - fast"
when
(exists "650.a.Indians of Mexico\\\\.")
then
addField "650.a.Indigenous peoples -- Mexico"
end

rule "Indigenous SH - Indian gays"
when
(exists "650.a.Indian gays")
then
addField "650.{-,7}.a.Two-spirit people"
end

rule "Indigenous SH - Indian gays - fast"
when
(exists "650.a.Indian gays\\\\.")
then
addField "650.{-,7}.a.Two-spirit people"
end
~~~

## Rule 2 breaks the field into the correct subfields, makes the second indicator 7, and adds a $2 with our local source

~~~
Rule 2
rule "Indigenous SH - Enslaved Indigenous persons"
when
(TRUE)
then
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Enslaved Indigenous persons")
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Canada, Northern"
when
(TRUE)
then
addSubField "650.z.Canada, Northern" if (exists "650.{-,7}.a.Inuit -- Canada, Northern")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Canada, Northern")
replaceContents "650.a.Inuit -- Canada, Northern" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Greenland"
when
(TRUE)
then
addSubField "650.z.Greenland" if (exists "650.{-,7}.a.Inuit -- Greenland")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Greenland")
replaceContents "650.a.Inuit -- Greenland" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Northwest Territories"
when
(TRUE)
then
addSubField "650.z.Northwest Territories" if (exists "650.{-,7}.a.Inuit -- Northwest Territories")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Northwest Territories")
replaceContents "650.a.Inuit -- Northwest Territories" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Yukon"
when
(TRUE)
then
addSubField "650.z.Yukon" if (exists "650.{-,7}.a.Inuit -- Yukon")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Yukon")
replaceContents "650.a.Inuit -- Yukon" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Canada"
when
(TRUE)
then
addSubField "650.z.Canada" if (exists "650.{-,7}.a.Inuit -- Canada")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Canada")
replaceContents "650.a.Inuit -- Canada" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Newfoundland"
when
(TRUE)
then
addSubField "650.z.Newfoundland" if (exists "650.{-,7}.a.Inuit -- Newfoundland")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Newfoundland")
replaceContents "650.a.Inuit -- Newfoundland" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Inuit -- Newfoundland and Labrador"
when
(TRUE)
then
addSubField "650.z.Newfoundland and Labrador" if (exists "650.{-,7}.a.Inuit -- Newfoundland and Labrador")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Inuit -- Newfoundland and Labrador")
replaceContents "650.a.Inuit -- Newfoundland and Labrador" with "Inuit"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Indigenous peoples Central America - CA"
when
(TRUE)
then
addSubField "650.z.Central America" if (exists "650.a.Indigenous peoples -- Central America")
changeSecondIndicator "650" to "7"  if (exists "650.a.Indigenous peoples -- Central America")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.a.Indigenous peoples -- Central America")
replaceContents "650.a.Indigenous peoples -- Central America" with "Indigenous peoples"
correctDuplicateSubfields "650" "2"
end
 
rule "Indigenous SH - Indigenous peoples North America - NA"
when
(TRUE)
then
addSubField "650.z.North America" if (exists "650.a.Indigenous peoples -- North America")
changeSecondIndicator "650" to "7" if (exists "650.a.Indigenous peoples -- North America")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.a.Indigenous peoples -- North America")
replaceContents "650.a.Indigenous peoples -- North America" with "Indigenous peoples"
correctDuplicateSubfields "650" "2"
end
 
rule "Indigenous SH - Indigenous peoples South America - SA"
when
(TRUE)
then
addSubField "650.z.South America" if (exists "650.a.Indigenous peoples -- South America")
changeSecondIndicator "650" to "7" if (exists "650.a.Indigenous peoples -- South America")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.a.Indigenous peoples -- South America")
replaceContents "650.a.Indigenous peoples -- South America" with "Indigenous peoples"
correctDuplicateSubfields "650" "2"
end
 
rule "Indigenous SH - Indigenous peoples West Indies - WI"
when
(TRUE)
then
addSubField "650.z.West Indies" if (exists "650.a.Indigenous peoples -- West Indies")
changeSecondIndicator "650" to "7" if (exists "650.a.Indigenous peoples -- West Indies")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.a.Indigenous peoples -- West Indies")
replaceContents "650.a.Indigenous peoples -- West Indies" with "Indigenous peoples"
correctDuplicateSubfields "650" "2"
end
 
rule "Indigenous SH - Indigenous peoples Mexico - M"
when
(TRUE)
then
addSubField "650.z.Mexico" if (exists "650.a.Indigenous peoples -- Mexico")
changeSecondIndicator "650" to "7" if (exists "650.a.Indigenous peoples -- Mexico")
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.a.Indigenous peoples -- Mexico")
replaceContents "650.a.Indigenous peoples -- Mexico" with "Indigenous peoples"
correctDuplicateSubfields "650" "2"
end

rule "Indigenous SH - Indian gays"
when
(TRUE)
then
addSubField "650.2.University of Toronto Indigenous Metadata Project" if (exists "650.{-,7}.a.Two-spirit people")
correctDuplicateSubfields "650" "2"
end
~~~

## Rule 3 removes any duplicate fields that get created when running the normalization process

~~~
Rule 3
rule "remove duplicate 650 fields"
when
(TRUE)
then
correctDuplicateFields "650"
end
Normalization Rules for display
This change only affects the 650 fields (in Config > Manage Display and Local Fields > subject )

Norm rule for display
rule "Primo VE Display- Subject 650"
when
(MARC."650" has any "a-z" AND NOT
MARC."650".ind"2"  equals "2" AND NOT
MARC."650".ind"2"  equals "1"  AND NOT 
MARC."650".ind"2"  equals "3" AND NOT 
MARC."650".ind"2"  equals "6"  AND NOT 
    MARC."650".ind"2"  equals "7") OR 
    (MARC."650" has any "a-z" AND
      MARC."650".ind"2"  equals "7" AND
      MARC."650"."2" match "fast")

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
        create pnx."display"."subject" with TEMP"1"
end
~~~
