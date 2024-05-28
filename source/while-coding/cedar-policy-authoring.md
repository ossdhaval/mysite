# Cedar

## What is Cedar?
Cedar is two things. Language + specification for interpreter
Cedar is a language for defining permissions as policies, which describe who should have access to what. It is also a specification for evaluating those policies. 

## What is it used for?
Use Cedar policies to control what each user of your application is permitted to do and what resources they may access.

## PARC model

Works on `PARC` model:
- Principal: The user or the actor of the request
- Action: action to be taken (like CRUD actions)
- Resource: Subject of the request (like a photo, some data in the app or some feature)
- Context: Contextual info about the principal (like has the pricipal been authenticated etc)

## policy statement

Every policy statement must include an effect and a scope:

- The effect specifies whether this a permit or a forbid policy.
- The `scope = PAR`, scope specifies the principal[s], the action[s], and the resource[s] to which the effect applies.
- Optionally, the statement may also include one or more conditions in the form of `when` or `unless` clauses. Conditions help add the context in decision making.

Each principal and resource are identified by a type and id. Everytime you refer to a resource or principal, you have to mention the type and its id. For example, the type could be `user` and id could be `alice`.


Policy applicability: A policy is applicable if the scope matches that of the authorization request, and all conditions are met.

How engine evaluates the final effect: Cedar policies are evaluated by a Cedar evaluation engine. The engine considers a set of policy statements in response to an authorization request, and returns either an allow or deny decision. For the authorization request to be allowed, there must be at least one applicable permit statement and no applicable forbid statements. 
