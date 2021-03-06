# Survey - Token

### Demo Video: 
https://www.youtube.com/watch?v=UaWMneJLy9U

### Use-Case:
Have you ever taken a survey or review and not been rewarded for it? With Survey token we remove the middleman like SurveyMonkey and G2Crowd and redistribute the money to people taking the survey and adding reviews. In the arena for survey marketplace there are two major stakeholders. The person/company creating the survey and the person taking the survey. Usually the survey creator creates a paid survey on survey monkey or G2Crowd annd the person taking the survey is rarely rewarded. 

Survey Monkey is a billion dollar company and G2 Crowd is funded with 45M dollars. Very few surveyers/ reviewers are  rewarded in coupons. 

With Survey token running on NEO, we incentivize surveyers with SUR token. SUR tokens are bought by the survey lister. 


### Flow:
Person/Company listing a survey would create a list of questions using the survey-frontend using surveyjs.
Once he/she completes it, he/she is asked to enter amount of NEO/GAS to transfer and number of people he/she wants to fill the survey.

For the sake of an example, lets say he/she sends 10 GAS and wants 100 people to fill the survey.

After the surveyer fills the review he will receive 10/100 = 0.1 GAS worth of tokens.

Currently 1 GAS = 40 SUR Tokens
          1 NEO = 100 SUR Tokens

### Stack

 - Smart Contract: https://github.com/melvin0008/survey-token
 - Frontend: https://github.com/melvin0008/survey-frontend
 - Backend: https://github.com/melvin0008/survey-token/blob/master/api.py


## Dapp Usage:

TestNet Hash: 0x46486fc3149a9c4074d67421528c58da9d7f0285 -> Latest

CozNet Hash: 0xd4903b35332d2a652f126ea6a978c179994321b3 (Old one)

### Functions available:
Name, symbol, decimals, balanceOf, transfer, transferFrom, totalSupply, approve and allowance and other NEX template functions.

Since this is a market place where in there are two sides.
 - Surveyer
 - Survey Lister

*After importing token to wallet*
import token 0x46486fc3149a9c4074d67421528c58da9d7f0285

The person creating the survey will invoke the function

`testinvoke 0x46486fc3149a9c4074d67421528c58da9d7f0285 create_survey  ["<survey_id>", "<number_of_people to distribute to>"] --attach-gas=<GAS that will be redistributed>`

or

`testinvoke Ox46486fc3149a9c4074d67421528c58da9d7f0285 create_survey  [“<survey_id>”, "<number_of_people to distribute to>"] --attach-neo=<NEO that will be redistributed>`

Make sure NEO is a whole number.

Survey Id: The id of the survey with question.
Number of people to distribute the assets

`testinvoke 0x46486fc3149a9c4074d67421528c58da9d7f0285 reward  ["<survey_id>", "<address of surveyer>"]`

address of surveyer : will be the address of the person who will be rewarded.

## Backend
To query the same from the backend setup the backend with

1. Setup neo-python https://github.com/CityOfZion/neo-python/blob/master/README.rst

2. Clone backend
`git clone https://github.com/melvin0008/survey-token/` and create a copy this to neo-python folder

3. Create DB
`python contracts/utils/db_create.py`

3. Run app
` python contracts/api.py`

4. Setup neon-wallet-db and private-net if you want to test it on private net.
` https://gist.github.com/slipo/f18f1a0b5e6adb7b0bf172b93379d891`


Using Postman have access to few endpoints

1. Get Version
   `{APP_URL}/api/`

2. Get Balance
   `{APP_URL}/api/wallet/<Address>`

3. POST Survey
   `{APP_URL}/api/survey/
   body { json: JSON received from survey editor }`

4. GET Survey
   `{APP_URL}/api/survey/<surveyid>

5. POST Get rewarded after survey
   `{APP_URL}/api/reward
   body { survey_id: <surveyId>, reward_address: <Address of the surveyer>}`
 
 6. POST Result of Survey
   `{APP_URL}/api/result
    body { survey_id: <surveyId>, json: <Result Jsonn file>}`
   
 He/She will only be rewarded if survey id will have remaining tokens to redistribute.
 He/She can only take survey once. (TODO)
 
 Only survey metadata and transactions are stored in the blockchain.
 Survey questions and answers are stored in DB


### Roadmap and TODO list:
 - [] Change Backend from sqllite to MongoDB
 - [] Improve maths for carrying out the free tokensale.
 - [] Add Results page for admin to check results (GET)
 
 
 ### For DAPP Competition:
 
 Changes made after 25th Feb:
 1. Update to latest neo-python with python 3.6. Update neo-template too with this.
 2. Work on frontend and backend of the the product.
