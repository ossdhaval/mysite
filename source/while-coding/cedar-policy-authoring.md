# Cedar

## What is Cedar?
Cedar is two things. Language + specification for interpreter.

Cedar is a language for defining permissions as policies, which describe who should have access to what. 

It is also a specification for evaluating those policies. 

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

Each principal and resource are identified by a type and id (action doesn't have type, it is always `action`). Everytime you refer to a resource or principal, you have to mention the type and its id. For example, the type could be `user` and id could be `alice`.


Policy applicability: A policy is applicable if the scope matches that of the authorization request, and all conditions are met.

How engine evaluates the final effect: Cedar policies are evaluated by a Cedar evaluation engine. The engine considers a set of policy statements in response to an authorization request, and returns either an allow or deny decision. For the authorization request to be allowed, there must be at least one applicable permit statement and no applicable forbid statements. 

### Writting broader policies:

#### Broader actions using sets

Within the policy scope you can define sets for actions, but not principals or resources. You can not, for example, define a scope for a set of principals.

```
permit(
  principal == User::"alice", 
  action in [Action::"view", Action::"edit", Action::"delete"], 
  resource == Photo::"VacationPhoto94.jpg"
);
```

#### Broadening the policies by leaving undefined in scope

if you leave principal or action or resource undefined, then it applies to all the entities. For example, the policy below will apply to all the principals.

```
permit(
  principal, 
  action in [Action::"view", Action::"edit", Action::"delete"], 
  resource == Photo::"vacationPhoto.jpg"
);
```

#### broaden principals using roles

The other way to broaden the scope of a policy is to define it for a group of entities, rather than an individual entity. Principal groups provide us with a way to manage permissions using roles.

```
permit(
  principal in Role::"vacationPhotoJudges",
  action == Action::"view",
  resource == Photo::"vacationPhoto94.jpg"
);

```

Cedar engine will match the above policy with a request for principal as `bob`, action as `view` and resource as `vacationPhoto94.jpg`. But how does cedar engine know if the `bob` as principal is part of the role `vacationPhotoJudges`? That is done through passing the `entities` to cedar engine at the time of evaluation call, like below:

```
let decision = authorizer.is_authorized(&request, &policy_set, &entities);
```

What is entities json and what does it look like?

Entities JSON is data about the entities mentioned in the request. In this case, it is data about bob and his roles. See below:

```
[
    {
        "uid": {
            "type": "User",
            "id": "Bob"
        },
        "attrs": {},
        "parents": [
            {
                "type": "Role",
                "id": "vacationPhotoJudges"
            },
            {
                "type": "Role",
                "id": "juniorPhotographerJudges"
            }
        ]
    },
    {
        "uid": {
            "type": "Role",
            "id": "vacationPhotoJudges"
        },
        "attrs": {},
        "parents": []
    },
    {
        "uid": {
            "type": "Role",
            "id": "juniorPhotographerJudges"
        },
        "attrs": {},
        "parents": []
    }
]

```

As you can see above, the Bob's user entity has a parents. Two roles. Both roles are also defined in the same JSON. Since `vacationPhotoJudges` is parent to Bob, the cedar engine interpretes this as bob having the role of `vacationPhotoJudges` and the policy will match the request for bob accessing the photo.



## References

- https://github.com/cedar-policy
