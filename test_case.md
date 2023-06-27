### client_id list
```ts
const rea = [  

];  
  
const rca = [  
  
]
```

## case1

### pre condition 

 - [ ] login as a `rca` users
 - [ ] haven't checked `hasSourceChecked` before
 - [ ] has `sourceRecord` in DB

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

- [ ]  no match `source_name`  -> no match `client_id`

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
sourceRecord: {
	source_name: rca_not_existed
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
