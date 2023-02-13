# serv-cda-allstack
serv-cda-allstack to manage all tech stacks of JoeyDoctor technology

## JoeyDoctor (JD) technology management platform
Current JD technology stacks consist of these following microservices:

 Dataprocess-expert (tentative name change to CDA-directory)

|-- model - port 5050 (map https://dataprocess.optimizecare.com, https://dataprocess.checkup.in.th/)

|-- controllog - port 5053

 Expert (tentative name change to CDA-model-expert)

|-- model - port 5000 (map https://expert.optimizecare.com)

|-- controllog - port 5003 

 CDA-ml (tentative name change to CDA-model-ml)

|-- model

|-- controllog

 CDA (tentative name change to CDA-model-clinical)

|-- gateway

|-- summary

|-- dataprocess-agent

|-- controllog

## Current issues
1. The repositoroes were not well designed for collaborative work, due to architecture designs, embeded libraries.
2. There are no independent databases, all configs were embeded into the code.
3. All codes need to be rebuilt each time there were some minor updates or patch.
4. No single management platform to configure.

## Solutions
### Existing services
1. CDA-directory
- convert var .py to json
- link json library (L123, Map items) to NoSQLDB
- as collection schema
- db: ocare_cda_directory, collection: directory_model_level 1 2 3, document: list of items

- lab mapping system, each L3 item contains hospital and hospital code and name
--- collection: 
" 
---- documents :
{
	"l3name": "name",
	"l3code": "name",
	"map": [{
		"hospitalname": "cuhc",
		"mapped_codename": [{
			"code": "codeis",
			"name": "nameis"
		}, {
			"code": "codeis",
			"name": "nameis"
		}]
	}]
}

scenario 1 hosp
1 lv3
- query document in collection which code = and name =
2. for i in map if hospital name == cuhc
return list of
{
		"hospitalname": "cuhc",
    "Uric acid": [
      "C0320",
      "C120",
      "C1729"
    ],
	"stool color": [
		"E1020"
	]
	}


2.1 for i in hospital name =  'cuhc'



- db: ocare_cda_directory, collection: directory_model_level 1 2 3, document: list of items

2. CDA-model-expert
- convert var .py to json
- link json library (L2, library) to NoSQLDB
- db: ocare_cda_expert, collection: expert_model_ a b c (normal, abn, bord, unde, L3, L3), document: list of items
3. CDA-model-ml

- as collection schema
-  db: ocare_cda_ml, collection: ml_model_ a b c (Level 2 name), document: list of items
- link json library (L2, library) to NoSQLDB

4. CDA-model-clinical
- (done) call model from NoSQLDB
- db: ocare_cda_clinical, collection: clinical_model_ ..., document: list of items

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
