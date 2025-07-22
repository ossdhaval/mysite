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

#### broaden principals using roles (RBAC)

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


In short, to broaden the scope:

- Leave principal, action, resource blank. Blank means `*`
- Additionally, actions can be broadened by using sets, while principal can be broadened by using role


#### Attribute based access control (ABAC)

The policy below permits any principal to view any resource, but only on the condition that the accessLevel for the resource is designated as public. It permits any principal to view any photo, but only on the condition that the resource is tagged as public and the location of the principal is equal to "USA".

```
permit(
  principal,
  action == Action::"view",
  resource
)
when {resource.accessLevel == "public" && principal.location == "USA"};
```

With entity json as:

```
{
        "uid": {
            "type": "Photo",
            "id": "VacationPhoto94.jpg"
        },
        "attrs": {
            "accessLevel": "public"
        },
        "parents": []
    },
    {
        "uid": {
            "type": "User",
            "id": "alice"
        },
        "attrs": {
            "location": "USA"
        },
        "parents": []
    }

```

Operators available for condition:

- &&
- ||
- ==

The example above uses an attribute of type String. Cedar can also support the following types:

- Boolean
- Integer
- Entity ID: eg. User::"Alice"
- Sets: collections of values, expressed with []
- !=

**Define conditions that compare the values of different attributes**:

```
permit(
  principal, 
  action in [Action::"view", Action::"edit", Action::"delete"], 
  resource 
)
when {
  resource.owner == principal.id
};
```

#### Context record

In the examples so far we’ve examined policies based on attributes of the principal and/or the resource. But what if you wanted to write a policy that takes takes into account variables that are unrelated to either the principal or the resource? Cedar provides a way for you to do this, using the Context record. Context enables you to pass additional data into the authorization request, **which can be referenced in policy conditions**.

Examples of context data you might use are OpenID claims in a JWT or anything else that is only known at the time of the incoming request and **not necessarily stored in your database**.

In prior examples our conditions have all been evaluated against static values. Cedar also lets you define conditions that compare the values of different attributes. The example policy below permits any principal to view, edit or delete, any resource, with the condition that the resource owner is the principal.

The policy below permits a User called Alice to update and delete a photo called VacationPhoto94.jpg, but only on the condition that she has authenticated using multi-factor authentication and is accessing the application from a specific IP address.

```
permit(
    principal in User::"alice", 
    action in [Action::"update", Action::"delete"],
    resource == Photo::"flower.jpg")
when {
    context.mfa_authenticated == true &&
    context.request_client_ip == "222.222.222.222"
};
```

The context and entities parameters of the request are different. The entities parameter enables the calling application to provide data about the resource and principal, such as attribute values and group membership. Context provides a mechanism for you to write policies that consider other data beyond that of the principal and resource.


### schema

Cedar can validate policies against the schema. Remember, schema is for validation of the policy and not the authz request.

A schema is a formal declaration of the names and structure of your entity types. You declare the name of each type of principal, resource, and action that your application supports. The definition of those entities can also include a list of the attributes that define an entity of that type, with each attribute specifying a name and a data type. Schema is not a must but it can help you make policy evaluations less error prone. 

A schema is defined by using JSON. Schemas have three main properties:

- Namespace: uniquely identifies the schema. The namespace helps you distinguish between elements with the same name from multiple schemas, for example HRApp::File and MedicalRecordsApp::File. The namespace is expressed as the top level key of the schema. Within each namespace, there is a JSON object defining entityTypes, actions, and types.
- entityTypes: defines the principal types and resource types supported by your application. Each entity type defines a shape that describes its characteristics. The shape must specify a Cedar supported data type, and define the structure for the more complex types like records or sets. The entity can also specify an optional memberOf attribute to describe how this type can participate in a hierarchy, like files can be in folders, users can be members of groups, or photos can be organized in albums. Note that if you specify that an entity can be a member of its own type, then you are specifying that you can nest them, such as placing folders in other folders.
- actions: defines the operations that the principals can potentially perform on the resources. Each action defines a name for the action, and a list of the resources and principals to which the action can apply.
- commonTypes: defines type aliases for complex record types in the schema. Pre-defining types allows for code re-usability whenever the same type is referenced in multiple entities. This key is optional.


Example:

```
{
    "PhotoApp": {
        "commonTypes": {
            "PersonType": {
                "type": "Record",
                "attributes": {
                    "age": {
                        "type": "Long"
                    },
                    "name": {
                        "type": "String"
                    }
                }
            },
            "ContextType": {
                "type": "Record",
                "attributes": {
                    "ip": {
                        "type": "Extension",
                        "name": "ipaddr"
                    }
                }
            }
        },
        "entityTypes": {
            "User": {
                "shape": {
                    "type": "Record",
                    "attributes": {
                        "employeeId": {
                            "type": "String",
                            "required": true
                        },
                        "personInfo": {
                            "type": "PersonType"
                        }
                    }
                },
                "memberOfTypes": [
                    "UserGroup"
                ]
            },
            "UserGroup": {
                "shape": {
                    "type": "Record",
                    "attributes": {}
                }
            },
            "Photo": {
                "shape": {
                    "type": "Record",
                    "attributes": {}
                },
                "memberOfTypes": [
                    "Album"
                ]
            },
            "Album": {
                "shape": {
                    "type": "Record",
                    "attributes": {}
                }
            }
        },
        "actions": {
            "viewPhoto": {
                "appliesTo": {
                    "principalTypes": [
                        "User",
                        "UserGroup"
                    ],
                    "resourceTypes": [
                        "Photo"
                    ],
                    "context": {
                        "type": "ContextType"
                    }
                }
            },
            "createPhoto": {
                "appliesTo": {
                    "principalTypes": [
                        "User",
                        "UserGroup"
                    ],
                    "resourceTypes": [
                        "Photo"
                    ],
                    "context": {
                        "type": "ContextType"
                    }
                }
            },
            "listPhotos": {
                "appliesTo": {
                    "principalTypes": [
                        "User",
                        "UserGroup"
                    ],
                    "resourceTypes": [
                        "Photo"
                    ],
                    "context": {
                        "type": "ContextType"
                    }
                }
            }
        }
    }
}
```

## References

- https://github.com/cedar-policy
