# subject-heading-masking

**TL;DR** Offensive Library of Congress subject headings were masked in the University of Toronto's LibrarySearch to display more appropriate terms. However, some electronic resource records (CZ bibs and CDI records) will not have the changes applied to them. Additionally, there are limitations with how subject searching works with some subject strings. This project is a response to offensive subject headings that display to our users in the catalogue, and it requires a 2-part solution. The first part is to "mask" certain Library of Congress Subject Headings (LCSH) with more appropriate terms in the LibrarySearch display, and the second part is to add uncontrolled index terms to ensure that they are searchable in LibrarySearch.

## Summary of the Project

This project is a response to offensive subject headings that display to our users in the catalogue, and it requires a 2-part solution. The first part is to "mask" certain Library of Congress Subject Headings (LCSH) with more appropriate terms in the LibrarySearch display, and the second part is to add uncontrolled index terms to ensure that they are searchable in LibrarySearch. Specifically, we have began by addressing the following terms:

|LCSH|New Term|Notes
|---|---|---|
|Indian slaves|Enslaved Indigenous persons||
|Indians of Central America|Indigenous peoples – Central America||
|Indians of Mexico|Indigenous peoples – Mexico||
|Indians of North America|Indigenous peoples – North America||
|Indians of the West Indies|Indigenous peoples – West Indies||
|Indians of South America|Indigenous peoples – South America||
|Eskimos--Canada, Northern|Inuit – Canada, Northern|Eskimo is the term that had been used by Library of Congress and other governmental bodies that encompasses distinct Indigenous peoples, often including the Inuit, Aleut, Chukchi, and the Yupik peoples. In Canada, the term Eskimo is considered derogatory, and the term Inuit is preferred. However, Inuit (which means people in Inuktitut) is not a word in the other languages, and therefore is not appropriate to apply without the context of a geographic subdivision.|
|Eskimos--Greenland|Inuit – Greenland||
|Eskimos--Northwest Territories|Inuit – Northwest Territories||
|Eskimos--Yukon|Inuit – Yukon||
|Eskimos--Canada|Inuit – Canada||
|Eskimos--Newfoundland|Inuit – Newfoundland||
|Eskimos–Newfoundland and Labrador|Inuit – Newfoundland and Labrador||
|Indian gays|Two-spirit people||


Note: When determining new terms to use, we have referenced the University of Manitoba LCSH Changes in MAIN, the [CRKN Interim Indigenous Subject Headings](https://docs.google.com/spreadsheets/d/1uPI55rpGEQT7OP3uJWVm2KWZ0RpaznaW/edit?gid=466199250#gid=466199250), and the [SACO Summary of Decisions}(https://www.loc.gov/aba/pcc/saco/cpsoed/psd-211018.html), editorial meeting number 2110 (for Enslaved persons). In the future we may also consult the [First Nations, Métis, and Inuit – Indigenous Ontology (FNMIIO)](https://docs.google.com/spreadsheets/d/e/2PACX-1vSOKcm9HB-28iSqNN3sQd5hV7bMLMGpCeGL0dkQgyg2AiZAMWUF0sp98GyxIvLXYIWqSZ3nX_j_q4UN/pubhtml) from NIKLA (currently in draft form) or other documents.

Our solution, allows us to not rely entirely on editing the metadata records, but instead to update how the terms display in LibrarySearch. This is because we also want to be part of the change to push LCSH to update their terms, at which point our records can also be "flipped" to the new LCSH terms in the metadata as well. 

## Part 1: Masking the display
To see how the display masking works, you should look at the details section of a result in LibrarySearch, and you will see that the subjects section will include the new term, not the LCSH one, regardless of whether the subject is only one of the term listed above (i.e. "Indigenous Peoples – Central America") or whether it is a longer string (i.e. "Indigenous peoples -- Mexico -- Anthropometry -- Mexico -- Veracruz-Llave (State) -- Congresses"). If you click through to the MARC view though, you will still see the original LCSH term.

## Part 2: Adding new indexed terms
The second part of the solution is that we needed to ensure that the subject index was picking up those records if users searched for the new term.

From our conversations with ExLibris, we learned that the way that the PrimoVE (a.k.a. LibrarySearch) subject search index works is to take metadata directly from the 65X fields of the bibliographic record, and to index those, not the new display terms. The subject search index can't be customized by us, because it is also is connected to the LCSH authority records. Some of these authority records contain only the LCSH term, but others contain a "see also" note, which includes the same new term that we've introduced. Because of these differences in authority records and the way that the search index is built, it meant that without further intervention, users would see smaller numbers of results if they searched the new term that they saw displayed (i.e.  "Indigenous Peoples – West Indies – Civil rights") , because the display fields weren't the ones being indexed, instead it was the original LCSH terms.

To get around this, we have added a topical subject field (marc field 650) to eligible bibliographic records, which contains the "root" new term for any of the LCSH terms that are also in the record. It is worth noting that it was not feasible to reconstruct the entire string in the new 650 (i.e. "Indigenous peoples -- North America -- Civil rights -- History"), but we were able to add the new root term "Indigenous peoples -- North America". These fields will have a subfield 2, which indicates that the source of the term is "University of Toronto Indigenous Metadata Project".

However, not all bib records are eligible for these changes though, which brings us to the limitations....

## Limitations
There are 2 limitations to this project:

1. These changes do not affect some electronic resource records. For electronic resources we have local bibliographic records (these will be affected by the display and index solutions), Community Zone (CZ) bibliographic records which are shared between all institutions using Alma, and Central Discovery Index (CDI) records which are predominantly book chapters and articles, similar to what summon used to be. Neither CZ bibliographic records or CDI records will have the new 650 fields, and therefore may be missed in the subject search if you use the new term and not the original LCSH. In addition, CDI records come in to LibrarySearch a different way, and so the masking will not work on them either. 
2. The linked subject headings may not always be helpful. What this means is that a user can search and find a record in LibrarySearch, and then see the details area of the record and click on the subject to see all the other items that share that subject. However, the way this process works technically is that it is using the display term to create a new subject search in LibrarySearch, and so if the full string isn't something that's directly in the bibliographic record or the 450/550 field in the authority record, they will get no results (i.e. clicking on Indigenous peoples -- South America -- Andes Region -- History in this record: https://utoronto-psb.primo.exlibrisgroup.com/permalink/01UTORONTO_INST/mbv7o/alma991106732738306196 ).
