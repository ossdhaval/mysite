# Cedar

## What is Cedar?
Cedar is two things. Language + specification for interpreter
Cedar is a language for defining permissions as policies, which describe who should have access to what. It is also a specification for evaluating those policies. 

## What is it used for?
Use Cedar policies to control what each user of your application is permitted to do and what resources they may access.

## Details

Works on `PARC` model:
- Principal: The user or the actor of the request
- Action: action to be taken (like CRUD actions)
- Resource: Subject of the request (like a photo, some data in the app or some feature)
- Context: Contextual info about the principal (like has the pricipal been authenticated etc)
