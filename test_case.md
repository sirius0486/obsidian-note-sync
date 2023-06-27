### client_id list
```ts
const rea = [  
'1slo5q0g99ss1e5cfctkdj3ni6',  
'63b4th825kkloal0u0b677vahs',  
'2fb06dqab95hci46dgldph0382',  
'67itphfaasklu3uo5htb953r04',  
'3b13kuk1s7s18c5olh3t3o2jmt',  
'4ccqj6b2b9439q7tdctvmlrdne'  
];  
  
const rca = [  
'1p48kcl0ftem2iee52ih34034',  
'5j47i153ecsr36fmsut62oe1c6',  
'6q3ro4100mm73lp5pbrq7rdj5h',  
'4pe9tnm1ob1g9e94a08itldueg',  
'49jott98s687hs7979ic5dm0l0',  
'2i429vaqutmpits0itbluc4fh3'  
]
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
sourceRecord: {
	source_name: rca
	source_id_: 8b88dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: E:lkay2333+dev1@gmail.com
}

// auth0 users
app_meatadata {
	lockeId: 666666,
	// hasSourceChecked:{
	//    rca: undefined
    // }
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
| sourceRecord     |  ❌  | has `sourceRecord` in DB            |

- [ ]  no match `source_name`  -> no match `client_id`

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	lockeId: 666666,
	// hasSourceChecked:{
	//    rca: undefined
    // }
}

```

### output
 - [ ] should not include `SourceInfo` in token  


## case3

### pre condition 

- [ ]  login as a `rca` users
 - [ ] has checked `hasSourceChecked` before
 - [ ] has `sourceRecord` in DB

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
sourceRecord: {
	source_name: rca
	source_id_: 8b88dcae-2e84-4989-bd59-9d517a00d5e5 
	email_or_lockeId: L: 666666
}

// auth0 users
app_meatadata {
	lockeId: 666666,
    hasSourceChecked:{
	    rca: true
    }
}

```

### output
 - [ ] should not include `sourceInfo` in token  


## case4

### pre condition 

- [ ]  login as a `rca` users
- [ ]  doesn't have checked `hasSourceChecked` before
- [ ]  doesn't have `sourceRecord` in DB

test_email : lkay2333+not_exist@gmail.com

### pre data

```ts
sourceRecord: {
	// empty
}

// auth0 users
app_meatadata {
	lockeId: 666666,
     // empty
    //hasSourceChecked:{
	
    //}
}

```

### output
 - [ ]  should not include `SourceInfo` in token
 - [ ]  only need to set `hasSourceChecked to true` like :
```ts
app_meatadata {
    hasSourceChecked:{
		rca: true
    }
}
```


## case5

### pre condition 

- [ ]  login as a `rca` users
- [ ]  haven't checked `hasSourceChecked` before
- [ ]  face error when get source record ( deploy `aws-bridge` older version , endpoint didn't exist, would throw error )

test_email : lkay2333+not_exist@gmail.com

### pre data

```ts

// auth0 users
app_meatadata {
	lockeId: 666666,
    
    hasSourceChecked:{
	
    }
}

```

### output
 - [ ]  throw error 
