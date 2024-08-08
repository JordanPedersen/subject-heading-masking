# Checklist for Go-Live
1. Create normalization rule for display in prod (see normalization-rule.md for the section of the rule that was modified)
2. Create bib normalization rule in prod (see bib-norm-rules.md)
3. Create the normalization process
4. Run normalization process on set of all bib records that only have physical inventory or local electronic bibs to add new new 650 fields (this change cannot be added to Community Zone records)
5. Add normalization process to MARC Normalization on Save
6. We also opened IdeaExchange with ExLibris asking for the masking to work with CDI titles: [IdeaExchange suggestion](https://ideas.exlibrisgroup.com/forums/308176-primo/suggestions/45251125-extend-subject-heading-display-masking-to-cdi-reco) now available for voting

## 1. Create Normalization Rule for Display
These steps rely on the [PrimoVE Normalization Rules for Display](https://knowledge.exlibrisgroup.com/Primo/Product_Documentation/020Primo_VE/Primo_VE_(English)/050Display_Configuration/Configuring_Normalization_Rules_for_Display_and_Local_Fields) documentation.
1. Navigate to the Display Fields page (Configuration Menu > Discovery > Display Configuration > Manage Display Fields). For UTL sandbox, I selected the field "subject" that was already in place.
2. Depending on your supported formats, edit the normalization rule row for the display field (for example, Marc21 Normalization Rule for display)
3. Modify the rules (see normalization-rule.md for the section of the rule that was modified). Our process mirrors the [SUNY documentation](https://public.3.basecamp.com/p/kDKKyiB88FQwGdUzL4vSrMGG)
4. Ensure that "apply rules" is checked after changes have been made.

### 2. Create Bib Normalization Rule
Use the [ExLibris New Normalization Rule Steps](https://knowledge.exlibrisgroup.com/Alma/Product_Documentation/010Alma_Online_Help_(English)/Metadata_Management/016Working_with_Rules/020Working_with_Normalization_Rules#To_create_a_new_normalization_rule_file). This process requires creating 3 normalization rules. See bib-norm-rules.md for the 3 rules.

## 3. Create Normalization Process
Use the [ExLibris Normalization Process Steps](https://knowledge.exlibrisgroup.com/Alma/Product_Documentation/010Alma_Online_Help_(English)/Metadata_Management/210Metadata_Management_Configuration/Configuring_Cataloging#Working_with_Normalization_Processes). Ensure that the 3 bib normalization rules are in order.

## 4. Run Normalization Process
We created a set of all local bib records that contained the subject headings that would be effected. This can be broken down into smaller sets if you're worried about run time / timing out.

## 5. Add Normalization Process to MARC Normalization on Save
This ensures that for new records that are brought in to Alma that the rule will be applied automatically on saving the record.
