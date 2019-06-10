# UIPath Client Security Hash- Data Scraping Project

This project is conducted within ACME Systems Inc. , Finance and Accounting Department.
The Objective of this process automation is intented to

* Deliver fast processing
* Reduce redundant activities
* Improve overall performance and reliability
## Process Description

Step.1 Open ACME System 1 Web Application
Step.2 Log into application with required username and password
Step.3 Access the work items menu in the dashboard
Step.4 For each activity of type WI5 perform the following steps
Step.5 Open the details page and retrieve the Client Information Details
Step.6 Open SHA 1 Online webpage
Step.7 Enter ClientID-ClientName-ClientCountry details
Step.8 Retrieve Client Security Hash value
Step.9 Go back to Client Information Details and update with hash value as comment and set status value to "Completed"
Step.10 Continue with next activity with type WI5

## Note
  - Orchestrator Queue is used to store Credentials
  - Robotic Enterprise Framework is used(REFramework)

[ReFrameWork Documentation](https://github.com/UiPath/ReFrameWork)






### Documentation is included in the Documentation folder ###

[ReFrameWork Documentation](https://github.com/UiPath/ReFrameWork)

### ReFrameWork Template ###
**Robotic Enterprise Framework**

* built on top of *Transactional Business Process* template
* using *State Machine* layout for the phases of automation project
* offering high level exception handling and application recovery
* keeps external settings in *Config.xlsx* file and Orchestrator assets
* pulls credentials from *Credential Manager* and Orchestrator assets
* gets transaction data from Orchestrator queue and updates back status
* takes screenshots in case of application exceptions
* provides extra utility workflows like sending a templated email
* runs sample Notepad application with dummy Excel input data
* 


### How It Works ###

1. **INITIALIZE PROCESS**
 + *InitiAllSettings* - Load config data from file and from assets
 + *InitiAllApplications* - Login to applications as per Config("OpenApps") field
   + *GetAppCredentials* - From Orchestrator assets or local Credential Manager
 + If failing, retry a few times as per Config("ProcessRetries")

2. **GET TRANSACTION DATA**
   + ./Framework/*GetTransactionData* - Fetches from Orchestrator queue as per Config("TransactionQueue")
   + ./*GetTransactionData* - Sample for working with Excel input files

3. **PROCESS TRANSACTION**
 + Try *ProcessTransaction*
 + If application exceptions happen
   + *SaveErrorScreen* - In Config("ErrorsFolder") with the exception message
   + Going to re/INITIALIZE
 + *SetTransactionStatus* - As Success, Failed or Rejected with reason
   + ./Framework/*SetTransactionStatus* - Updates the Orchestrator queue item
   + ./*SetTransactionStatus* - Sample for updating Excel input file

4. **END PROCESS**
 + *CloseAllApplications* - As listed in Config("CloseApps")


### For New Project ###

1. Check out the Config.xlsx file and add/customize any required fields and values
2. Implement OpenApp and CloseApp workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData and SetTransactionStatus or use ./Framework versions for Orchestrator queues
4. Implement ProcessTransaction workflow and any invoked others
