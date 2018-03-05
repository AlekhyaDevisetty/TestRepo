# Two Way Sync Documentation
#### Problem Statement :
Analysing a scenario where user can perform operations using Two Way sync where actions can be performed online and offline.
#### Approaches :
1. Log Based Approach
2. Flag Based Approach
3. Timestamp Based Approach
#### Approach we adopted :
We opted for a Timestamp based appproach, in which we will maintain timestamps for each record which helps us to find the solution for this problem. 
Our solution comprises of five projects
1. ClientApp.Console
2. Server App
3. Two_way_sync_Domain_Model
4. Two_way_sync_client
5. Two_way_sync_server

Two_way_sync_domain model consists of base model for the client tables and api. Both two_way_sync_client and two_way_sync_server makes use of Two_way_sync_Domain_model.

Two_way_sync_client is the dll file which will be provided to the user. This consists of 
1. main sync logic which resolves all the conflicts.
2. Model classes for Sync Settings( which has the meta data of the tables present in client database).
3. Client side database operations(IDBOperations and SQliteDB Operations).

Two way sync server is an other dll file which handles with the server side operations
1. Consists of a Sync Controller which has Get and Post methods for handling data.
2. Server side dboperations are also handled here.

Client App.Console is the project which a user needs to write.
Here the user should add references of Two way sync client and Two way sync Domain model.
1.User can create as many tables he want by inherting ISyncBase Model class. Now that they need to initialize the constructor of Sync class and call StartSync method to sync data.
2.When ever user creates a table in client app they need to enter the meta data about the table like AutoSync, Priority in Sync Settings table.

Server app should be coded by the user. Here they writes controllers for their respective tables. In this area he can levy conditions on the data and retrieve the required data they need. 

#### Finished :
1. Sync logic
2. Providing priorities to user(enum : If 0 - Last Modified records will be reflecting in both the databases. 1 -- Server changes will be reflected during conflicting situations. 2--  Client changes will be reflected during conflicting situations.
3-- User is again asked to choose one among the priorities.

### Yet to be finished :
1. Auto Sync
2. Hard and Soft Delete where we need to add two more attributes in the sync settings table.
3. Should figure out a proper way to interact with the database if the user selects the priority number 3 i.e User priority.
4. Solving GUID replica conflicts
5. Provising of cascading mechanism which should be implemented internally.
6. Sync mechanism for multiple tables in a given sequence.
7. Globalising variables which will be passed to the server.
8. Parellel syncing.
9. Testing for 5000 records.
10. Time calculation for sync process.

