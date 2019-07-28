# CodeFunDo_theNAPteam
# e-Elections using Blockchain

### Introduction 

India being the largest democracy in the world caters to a huge population, conducts innumerous elections and has polling booths across 29 states and union territories at multiple tiers. Referenda and polls are very important processes & tools for the smooth operation of a modern democracy.

Some of the key problems in such a widely conducted activity are rigging of polling booths, bribery and use of money power to buy votes and low voter turnouts. This significantly affects the candidates fighting in the elections and might not result in a fair electoral process.   

Our solution demonstrates how you can make these processes more secure, reliable, and transparent using Azure Blockchain.

### Idea for CodeFunDo++

We plan to build a system comprising of: 

    1.  Automatic generation of voter card on turning 18

Now that AADHAR Card is mandatory for every citizen of the country this can be used as an effective database for the eligible voters in a constituency. The Ministry of Electronics and Information Technology (MeitY) which allocates AADHAR will automatically register all the new AADHAR Card holders to our system. A password will be provided to the respective users to log into the app, which is to be changed by the users after receiving it, to secure their accounts. The system henceforth will check for the age of the user by reading the AADHAR and provide automatic voting access on turning 18. Everyone who is 18+ on the system will be assigned an e-Voter Card in real time. 

This will help increase the turnout in elections as a lot of citizens do not make their voter cards given the long rigmarole of an offline application for the same. 

    2. Remote Voting Access

Our model now has an online database of all the eligible voters in the country. The system is an e-voting platform which is app and web based wherein a voter can sign in during elections to cast his or her vote. Unlike the current practice, wherein a person can only vote in the constituency where his/her address (as mentioned in the voter card) falls, our model allows a person to vote from anywhere in the country and even overseas. 

This will bring about a significant participation in the electoral process as this will allow people to vote in the click of a button or in the comfort of their homes. 

For a similar experience in rural areas with no or poor internet access, or unavailability of smartphones, mobile polling booths with desktops or smartphones should be installed for the people living nearby. 

For security reasons, the system will verify the user on many folds like password, OTP and facial recognition (by matching it to the AADHAR). During the voting process, the webcam of the user should be switched on at all times to videograph the entire process. There will also be MAC filtering for each device in the backend wherein devices used to cast multiple votes will be notified to the ECI (Election Commission of India) to check for and avoid illegitimate votes. 

    3. Expedite Vote Counting

Using the blockchain technology, the system automatically calculates the number of votes for each candidate (which is a node in our blockchain network). This is later fed to a software application with other details like the constituency id and party id to generate elections results quickly. 

This saves huge amounts of time and the need to transport EVMs from one place to another. This also rules down cases of EVM hacking and other malpractices while vote counting. 

    4. Financial Transparency

It often happens that major political parties have an obvious advantage where they can use an excess of money power to ‘buy’ votes with bribery. Even while campaigning, smaller parties have a disadvantage since they don’t have as much money or power as the bigger parties. The EIC sanctions a certain budget which a party needs to stick to, but there have been innumerous cases of exceeding it using black money. 

On our system, the EIC can give each political party some token budget which is visible on our application. This amount is then shown to be deducted virtually as and when the party performs real monetary expenditure. Here, we can keep a track of the purchases of the party and any purchase not highlighted on the application and caught in the public domain by the general people and media shall be then reported. 

### Technology

Our system uses Blockchain Technology provided by Microsoft in the following manner:

1.  We build and configure our underlying blockchain infrastructure using the Azure Blockchain Service where each node in the network is later initialised with each candidate standing for the election.

2.  We then use Visual Studio Code to author and test Smart Contracts which are written in Solidity that would be deployed to a consortium networking Azure Blockchain Service to public Ethereum. These smart contracts contain the logic of our application, including the rules that allow a person to vote justly. These rules are secure and can be changed only by the administrator, making the process secure.

Each candidate will be stored with multiple attributes about itself. The system keeps track of a candidate's id, name, and vote count. 

This Candidate struct is initialized with the candidate id, name and the initial vote count to 0. Note that this function's visibility is private because only the concerned authority will want to call it inside the contract.

>> contract Election {
>>   // Model a Candidate
>>    struct Candidate {
>>      uint id;
>>        string name;
>>        uint voteCount;
>>    }

The next thing to do is store the candidates, which is one of the structure types we have just created. We can do this with a Solidity mapping. (A mapping in Solidity is like an associative array or a hash, that associates key-value pairs).

>>  mapping(uint => Candidate) public candidates;
>>  uint public candidatesCount

Next, there is a function to add candidates to this mapping. 

>>  function addCandidate (string _name) private {
>>        candidatesCount ++;
>>        candidates[candidatesCount] = Candidate(candidatesCount, _name, 0);
>>  }


Now there are a few points regarding the ability to cast votes in the election. The core functionality of this function is to increase the candidate's vote count by reading the Candidate struct out of the "candidates" mapping and increasing the "voteCount" by 1 with the increment operator (++). 

Its visibility is public because we want an external account to call it.
It adds the account that voted for the voters mapping that we just created. This will allow us to keep track that the voter has voted in the election. We access the account that's calling this function with the global variable "msg.sender" provided by Solidity.

It implements require statements that will stop execution if the conditions are not met. First require that the voter hasn't voted before. We do this by reading the account address with "msg.sender" from the mapping. If it's there, the account has already voted. Next, it requires that the candidate id is valid.

3. We finally build an application on top of this ledger network that would write messages to and read messages off this ledger and route it to applications and databases with the Workbench Tool.
 









