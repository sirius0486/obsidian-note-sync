### client_id list
```ts
const MYREA_CLIENTS = [  
'1slo5q0g99ss1e5cfctkdj3ni6',  
'63b4th825kkloal0u0b677vahs',  
'2fb06dqab95hci46dgldph0382',  
'67itphfaasklu3uo5htb953r04',  
'3b13kuk1s7s18c5olh3t3o2jmt',  
'4ccqj6b2b9439q7tdctvmlrdne'
];  
  
const RCA_CLIENTS = [  
'1p48kcl0ftem2iee52ih34034',  
'5j47i153ecsr36fmsut62oe1c6',  
'6q3ro4100mm73lp5pbrq7rdj5h',  
'4pe9tnm1ob1g9e94a08itldueg',  
'49jott98s687hs7979ic5dm0l0',  
'2i429vaqutmpits0itbluc4fh3'  
]

'hQW11zQer3bjwcqk5ZxBRzZDTRgqEBt8'  // default client in locke_demo

```

## case1

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users |
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ✅  | has `sourceRecord` in DB            |


test_email : lkay2333+dev1@gmail.com

### pre data

```ts
// sourceRecord in DB
sourceRecord: {
	source_name: rca
	source_id_: 5b68dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: E:lkay2333+dev1@gmail.com
}

// auth0 users app_metadata
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
}

```

### output
 - [ ] updated sourceInfo in token  
 - [ ] set sourceChecked like     `app_meatadata { rca: true }`
 - [ ] update email to lockeId  `email_or_lockeId`

## case2

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ✅  | have checked `hasSourceChecked` before |
| sourceRecord     |  ✅  | have `sourceRecord` in DB         |

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
// sourceRecord in DB
sourceRecord: {
	source_name: rca
	source_id_: 5b68dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: E:lkay2333+dev1@gmail.com
}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
	    rca: true
    }
}

```

### output
 - [ ] should not include `sourceInfo` in token  

## case3

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ❌   | no match `source_name` |
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |  ❌  | can find sourceRecord         |

- [ ]  no match `client_id`  -> no match `source_name` 

test_email : lkay2333+dev3@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
}

```

### output
 - [ ] should not include `SourceInfo` in token  
 - [ ] `hasSourceChecked`  still empty

## case4

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ❌ | does not have `sourceRecord` in DB         |

test_email : lkay2333+dev4@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
}

```

### output
 - [ ]  should not include `SourceInfo` in token
 - [ ]  only need to set `hasSourceChecked to true` like :
```ts
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
		rca: true
    }
}
```


## case5

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users, but use  `myRea` client|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| SourceRecord     |   ❌ |  does not have `sourceRecord` in DB |


test_email : test_email : lkay2333+dev5@gmail.com

login as a `rca` users, but use  `myRea` client
- 1. add metadata in auth0 
- 2. replace client_id in auth0

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
		rca: true
    }
}

```

### output
 - [ ]  set  hasSourceChecked -  `myRea` to true
```ts
// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
		rca: true,
		myRea: true
    }
}
```

## case6

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| Encounter a error when getSourceRecord     |   ❌ | deploy `aws-bridge` older version , endpoint didn't exist, would throw error         |


test_email : test_email : lkay2333+dev6@gmail.com

deploy this version: [1b4c214](https://git.realestate.com.au/Locke/auth0-aws-bridge/commit/1b4c2144eee099e7be4c40192292465c2959196f)


### output
 - [ ]  throw  `InternalServerErrorException` error 



## UI client

https://settings.locke-dev.rea-group.com/delete?client_id=112lqg4crpvoi8a2nkr9de9lf7&redirect_uri=https://locke-demo.locke-dev.rea-group.com/profile

https://settings.locke-dev.rea-group.com/global-sign-out?client_id=112lqg4crpvoi8a2nkr9de9lf7&redirect_uri=https://locke-demo.locke-dev.rea-group.com/profile

https://settings.locke-dev.rea-group.com/delete?client_id=2i429vaqutmpits0itbluc4fh3&redirect_uri=https://locke-demo.locke-dev.rea-group.com/profile

### prod
default: LzSGQNnJ0x9xx8u9s252Yy0jLmY0mdzW

pT:  7fj1shu31fnrbgf8at0olfhm9q   

rca:   4pe9tnm1ob1g9e94a08itldueg 1p48kcl0ftem2iee52ih34034

https://settings-prod.locke-dev.rea-group.com/global-sign-out?client_id=7fj1shu31fnrbgf8at0olfhm9q&redirect_uri=https://locke-demo-prod.locke-dev.rea-group.com/profile

https://settings-prod.locke-dev.rea-group.com/forbidden.html


### dev
PT:     112lqg4crpvoi8a2nkr9de9lf7
RCA:  2i429vaqutmpits0itbluc4fh3 3b13kuk1s7s18c5olh3t3o2jmt

https://settings.locke-dev.rea-group.com/global-sign-out?client_id=112lqg4crpvoi8a2nkr9de9lf7&redirect_uri=https://locke-demo.locke-dev.rea-group.com/profile


https://settings.locke-dev.rea-group.com/forbidden.html



https://settings.locke-dev.rea-group.com/global-sign-out?client_id=112lqg4crpvoi8a2nkr9de9lf7&redirect_uri=https://locke-demo.locke-dev.rea-group.com/profile



```ts
import { Request, Response } from 'express';
import { pipe } from 'fp-ts/function';
import * as TE from 'fp-ts/TaskEither';
import { getUserSource } from '../services/userSourceService';
import { errorHandler } from './errorHandler';
import {ApiError, InvalidParameterError} from "../services/apiError";

type queryParams = {
  locke_id: string;
  email: string;
  source_name: string;
}

export const getUserSourceHandler = (request: Request, response: Response) => pipe(
  request.query as queryParams,
  TE.right,
  TE.filterOrElse<ApiError, queryParams>( ({ locke_id, email, source_name}) => !!email && !!locke_id && !!source_name,
    () => new InvalidParameterError('locke id , email and source_name are required.') ),
  TE.chain(( {locke_id, email, source_name}) => getUserSource( locke_id, email, source_name )),
  TE.map((userSourceRecord) => {
    response.status(200).send(userSourceRecord);
  }),
  TE.mapLeft((error) => {
    errorHandler(response, error)
  })
)();

import { QueryCommandInput, QueryCommandOutput, UpdateCommandInput, UpdateCommandOutput } from "@aws-sdk/lib-dynamodb";  
import * as TE from "fp-ts/TaskEither";  
import { ApiError } from "./apiError";  
import { pipe } from "fp-ts/function";  
import { DynamoDBClient } from "../clients/dynamoDBClient";  
import { handleError } from "./handleError";  
import config from '../utils/config';  
  
export type UserSource = {  
source_id: string;  
source_name: string;  
email_or_locke_id: string;  
}  
  
export const getUserSource = (locke_id: string, email: string, source_name: string): TE.TaskEither<ApiError, UserSource | undefined> => pipe(  
locke_id,  
getUserSourceInfoByLockeId,  
TE.chain<ApiError, UserSource | undefined, UserSource | undefined>((userSourceByLockeId) =>  
userSourceByLockeId ? TE.right(userSourceByLockeId) : pipe(  
getUserSourceInfoByEmail(email),  
TE.chain<ApiError, UserSource[] | undefined, UserSource | undefined>((userSources) => pipe(  
userSources,  
(userSources) => (userSources || []).find(user => user.source_name === source_name),  
(userSource) => userSource ? updateSourceAttributionsEmailToLockeId(userSource, locke_id) : TE.right(undefined)  
)  
)  
)  
));  
  
const getUserSourceInfoByLockeId = (locke_id: string): TE.TaskEither<ApiError, UserSource | undefined> => pipe(  
({  
TableName: config.userSourceAttributionsTable,  
IndexName: 'locke_id_index',  
KeyConditionExpression:  
"email_or_locke_id = :lockeId",  
ExpressionAttributeValues: {  
":lockeId": `L:${ locke_id }`,  
},  
}) as QueryCommandInput,  
new DynamoDBClient().query,  
TE.map<QueryCommandOutput, UserSource | undefined>(result => result?.Items?.[0] as UserSource | undefined ),  
TE.mapLeft(handleError(`Get user source info by locke id`))  
)  
  
const getUserSourceInfoByEmail = (email: string): TE.TaskEither<ApiError, UserSource[] | undefined> => pipe(  
({  
TableName: config.userSourceAttributionsTable,  
IndexName: 'locke_id_index',  
KeyConditionExpression:  
"email_or_locke_id = :email",  
ExpressionAttributeValues: {  
":email": `E:${ email }`,  
},  
}) as QueryCommandInput,  
new DynamoDBClient().query,  
TE.map<QueryCommandOutput, UserSource[] | undefined>(result => result?.Items as UserSource[] | undefined ),  
TE.mapLeft(handleError(`Get user source info by email`))  
)  
  
const updateSourceAttributionsEmailToLockeId = ( userSource: UserSource, lockeId: string ): TE.TaskEither<ApiError, UserSource> => pipe(  
({  
TableName: config.userSourceAttributionsTable,  
IndexName: 'locke_id_index',  
Key: {  
source_id: `${ userSource.source_id }`,  
source_name: `${ userSource.source_name }`  
},  
UpdateExpression: 'SET email_or_locke_id = :email_or_locke_id',  
ConditionExpression: 'begins_with(email_or_locke_id, :emailPrefix)',  
ExpressionAttributeValues: {  
':email_or_locke_id': `L:${ lockeId }`,  
':emailPrefix': 'E:'  
},  
ReturnValues: 'ALL_NEW'  
}) as unknown as UpdateCommandInput,  
new DynamoDBClient().update,  
TE.map<UpdateCommandOutput, UserSource>(( result ) => result.Attributes as UserSource ),  
TE.mapLeft(handleError(`update user source attributions email to locke_id`))  
)
```