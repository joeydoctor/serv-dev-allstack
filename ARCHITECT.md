## JoetyDoctor Technology
consists of 4 major and 2 minor microservices

### 1. serv-CDA-directory 
### 2. serv-CDA-model-expert
### 3. serv-CDA-model-clinical
### 4. serv-CDA-model-ml


### 5. serv-CDA-credential (to control credential of healthdashboard cuhc)
### 6. serv-CDA-allstack (to manage all tech stacks of JD technology)

- each microservice has its own log system which runs on gcp cloud server

System architecture
2 main servers
- server - Ubuntu GCP (use to store logs, event, no-need to scale app)
- serverless - Cloudrun (use for application which needs autoscale)

-- serv-CDA-directory 
---- dataprocess-controllog
---- dataprocess-model

-- serv-CDA-model-expert 
---- expert-controllog
---- expert-model (*** run on Cloud run serverless ***)

-- serv-CDA-model-clinical 
---- cda-controllog (*** run on Cloud run serverless ***)
---- cda-gateway
---- cda-summary (*** run on Cloud run serverless ***)
---- cda-dataprocess-agent

-- serv-CDA-model-ml 
---- cda-ml-bucket (*** run on Cloud run serverless ***)
---- cda-ml-model (*** run on Cloud run serverless ***)


7. serv-www >> move to micro server 1 cpu