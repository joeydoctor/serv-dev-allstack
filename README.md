# serv-cda-allstack
serv-cda-allstack to manage all tech stacks of JoeyDoctor technology

## JoeyDoctor (JD) technology management platform
Current JD services consist of these microservices:

 Dataprocess-expert (tentative change to CDA-directory)

|-- model - port 5050 (map https://dataprocess.optimizecare.com, https://dataprocess.checkup.in.th/)

|-- controllog - port 5053

 Expert (tentative change to CDA-model-expert)

|-- model - port 5000 (map https://expert.optimizecare.com)

|-- controllog - port 5003 

 CDA-ml (tentative change to CDA-model-ml)

|-- model

|-- controllog

 CDA (tentative change to CDA-model-clinical)

|-- gateway

|-- summary

|-- dataprocess-agent

|-- controllog

## Current issues
1. The repository is not well designed for collaborative work, due to arch designs, embeded libraryies.
2. All codes need o be rebuild each time there were some minor updates or patch
3. No single management platform to configure.

## Solutions
### Existing services
1. CDA-directory
- convert var .py to json
- link json library (L123, Map items) to NoSQLDB
- as collection schema
-  db: ocare_cda_dataprocess, collection: ocare_cda_model_level 1 2 3, document: list of items

2. CDA-model-expert
- convert var .py to json
- link json library (L2, library) to NoSQLDB
- db: ocare_cda_expert, collection: ocare_cda_model_expert_ a b c (Level 2 name), document: list of items each l2
3. CDA-model-ml

- as collection schema
-  db: ocare_cda_ml, collection: ocare_cda_model_ml_ a b c (Level 2 name), document: list of items
- link json library (L2, library) to NoSQLDB

4. CDA-model-clinical
- (done) call model from NoSQLDB
- db: ocare_cda, collection: ocare_cda_model_captures, document: list of items

### New cda-allstack services
serv-cda-allstack to manage all tech stacks of JoeyDoctor technology (*** in Database layer)

1.CDA-directory - systematic & itemized health items
 CRUD
 listed by display orders of
- L1
-- L2 (check if there is expert, cda-ml)
--- L3 (check if there is cda)

2.CDA-model-expert
 Linked L2 from CDA - dataprocessor (if exist show button)
  - CRUD item to list in document [normal_list, borderline_list, abnormal_list, notexamined_list]
  - CRUD item to dict in document { L3_ref/ L2_recommend_dict - diseasecapture, detail, interpret}
  
3.CDA-model-ml model ref from expert/ ca
 Linked L2 from CDA - dataprocessor (if exist show button)
  - CRUD collection of each model
  - CRUD item to document in each model
- link button to df/ to train
- link button to Push model to Bucket/ Deletion

4.CDA-model-clinical
 Linked L3 from CDA - dataprocessor (if exist show button)
  - CRUD collection of each model
  - CRUD item to document in each model
