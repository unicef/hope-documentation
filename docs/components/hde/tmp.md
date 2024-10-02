Deduplication 

 
 

 
 

RDI 

Fuzzy 

Threshold by BA 

 
 

 
 

Programme based deduplication. 

 
 

 
 

Check on documents happen after merge. 

 
 

 
 

 
 

CHANGE REQUEST 168410 

 
 

Customizable deduplication 

 
 

 
 

Real cases: 

Need adjudication: same "Bank Statement" number 

 
 

 
 

Duplicate 

Not Duplicate 

Withdrawn 

 
 

 
 

Not Withdrawn 

 
 

 
 

 
 

Deduplication  

what is the flag "Postpone deduplication”? 

status pending  

Document type flags 

is_identity_document 

valid_for_deduplication (change the signature ==> 2 valid document with same ID) 

document number 

 
 

 
 

 
 

Batch 

 
 

Golden Records 

 
 

Threashold -> need adjudication 

 
 

deduplication_batch_results  

deduplication_golden_record_results  

 
 

 
 

Questions 

 
 

A) what is the flag "Postpone deduplication" 

what would it stop? 

fuzzy match 

bank account 

document number 

 
 

Disable ES 

 
 

 
 

B) document type - valid_for_deduplication flag has it used? 

 
 

 
 

ok so deduplication works on all documents with: 

status pending  

flag is_identity_document set to true 

 
 

 
 

flag valid_for_deduplication only change the signature ==> 2 valid document with same ID 

 
 

 
 

 
 

DEDUPLICATION 

Name, gender, date of birth 

 
 

  

Flexible de-duplications checks (decide from user side which fields should be used to deduplicate) 

No, depends on filters, index 

Requires redesign of flex fields 

Redesign deduplication (?) 

 
 

 
 

Instructions: 

List: subset (aka sessions) 

 
 

 
 

 
 

 
 

is identity document 

if this is set to true, we use this document to deduplicate and create ticket 

 
 

unique for individual 

you cannot create more than one document of this type for individual 

 
 

valid for deduplication 

ignores the type of the document during deduplication and deduplicate between different types with this flag set to true 

 
 

 

There are two different rules for documents uniqueness: 

"unique for individual" flag indicates whether we should validate uniqueness of document type per individual - so that Individual can only have 1 VALID document of this document_type+country. 

document data uniqueness inside a Program - so that there cannot be more than 1 VALID document with the same set of values: document_number+type+country in a Program 

 