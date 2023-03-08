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
- Ubuntu server (use to store logs, event, no-need to scale app)
- Cloud run (use for application which needs autoscale)

-- serv-CDA-directory 
---- dataprocess-controllog
---- dataprocess-model

-- serv-CDA-model-expert 
---- expert-controllog
---- expert-model (*** run on Cloud run serverless ***)

-- serv-CDA-model-clinical 
---- cda-controllog
---- cda-gateway
---- cda-summary
---- cda-dataprocess-agent

-- serv-CDA-model-expert 
---- cda-ml-bucket
---- cda-ml-model