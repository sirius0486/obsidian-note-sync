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


test_email : lkay2333+dev@gmail.com

### pre data

```ts
// sourceRecord in DB
sourceRecord: {
	source_name: rca
	source_id_: 8b88dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: E:lkay2333+dev@gmail.com
}

// auth0 users
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
| sourceName       |   ❌   | no match `source_name` |
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |  ❌  | can find sourceRecord         |

- [ ]  no match `client_id`  -> no match `source_name` 

test_email : lkay2333+dev@gmail.com

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


## case3

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ✅  | have checked `hasSourceChecked` before |
| sourceRecord     |  ✅  | have `sourceRecord` in DB         |

test_email : lkay2333+dev@gmail.com

### pre data

```ts
sourceRecord: {
	source_name: rca
	source_id_: 8b88dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: L:54373d21-7a2d-56e6-9d2e-afaac50df33f
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


## case4

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ❌ | does not have `sourceRecord` in DB         |

test_email : lkay2333+dev@gmail.com

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
| sourceName       |   ✅  | login as a `rca` users|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| Encounter a error when getSourceRecord     |   ❌ | deploy `aws-bridge` older version , endpoint didn't exist, would throw error         |


test_email : test_email : lkay2333+dev@gmail.com

[1b4c214](https://git.realestate.com.au/Locke/auth0-aws-bridge/commit/1b4c2144eee099e7be4c40192292465c2959196f)

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
	
    }
}

```

### output
 - [ ]  throw error 

## case6

### pre condition 



| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| sourceName       |   ✅  | login as a `rca` users, rca use  myRea client|
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| Encounter a error when getSourceRecord     |   ❌ | deploy `aws-bridge` older version , endpoint didn't exist, would throw error         |


test_email : test_email : lkay2333+dev@gmail.com

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
 - [ ]  set myRea to true
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
