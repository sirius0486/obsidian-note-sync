### login url

> dev:  

rea: 3b13kuk1s7s18c5olh3t3o2jmt
rca: 2i429vaqutmpits0itbluc4fh3

https://id-dev.realestate.com.au/authorize?client_id=3b13kuk1s7s18c5olh3t3o2jmt&response_type=code&audience=default&scope=openid+profile+email+phone+offline_access&redirect_uri=http://localhost:3000&connection=email

prod:
rea:   1slo5q0g99ss1e5cfctkdj3ni6, 63b4th825kkloal0u0b677vahs
rca:  1p48kcl0ftem2iee52ih34034, 5j47i153ecsr36fmsut62oe1c6

https://id-dev.realestate.com.au/authorize?client_id=1p48kcl0ftem2iee52ih34034&response_type=code&audience=default&scope=openid+profile+email+phone+offline_access&redirect_uri=https%3A%2F%2Flocke-demo.locke-dev.rea-group.com%2Fauth%2Fcallback&connection=email


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
| lockeId       |   ✅  | users lockeId existed in DB |
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ✅  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 1p48kcl0ftem2iee52ih34034            |

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
// sourceRecord in DB called user-source-attributions
sourceRecord: {
	source_name: rca
	source_id_: test1001
	email_or_lockeId: L:a1d8f09a-030f-420d-abc0-65dc0d94044f
}

// auth0 users app_metadata
app_meatadata {
	lockeId: a1d8f09a-030f-420d-abc0-65dc0d94044f,
}

```

### output
 - [x] updated sourceInfo in token   ->  `test1001 &  rca`
 - [x] set `sourceChecked` like     `app_meatadata { clentID: true }`
 

## case2

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| lockeId       |   ✅  | users lockeId existed in DB |
| hasSourceChecked |   ✅  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ✅  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 1p48kcl0ftem2iee52ih34034            |

test_email : lkay2333+dev1@gmail.com

### pre data

```ts
// sourceRecord in DB
sourceRecord: {
	source_name: rca
	source_id_: test1001
	email_or_lockeId: L:a1d8f09a-030f-420d-abc0-65dc0d94044f
}

// auth0 users
app_meatadata {
	lockeId: 54373d21-7a2d-56e6-9d2e-afaac50df33f,
    hasSourceChecked:{
	    1p48kcl0ftem2iee52ih34034: true
    }
}

```

### output
 - [x] should not include `sourceInfo` in token  

## case3

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| lockeId       |   ❌  | users lockeId not existed in DB |
| hasSourceChecked |   ❌  | haven't checked `hasSourceChecked` before |
| sourceRecord     |   ✅  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 5j47i153ecsr36fmsut62oe1c6            |

test_email : lkay2333+dev2@gmail.com

### pre data

```ts
sourceRecord: {
	source_name: rca
	source_id_: test1002
	email_or_lockeId: E:lkay2333+dev2@gmail.com
}

// auth0 users
app_meatadata {
	 
}

```

### output
 - [x] should include `SourceInfo` in token 
 - [x] update `email` to `lockeId`
 - [x] appmeatadata: { `5j47i153ecsr36fmsut62oe1c6` : true }

## case4

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| lockeId       |   ❌  | users lockeId not existed in DB |
| hasSourceChecked |   ✅  | have checked `hasSourceChecked` before |
| sourceRecord     |   ✅  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 5j47i153ecsr36fmsut62oe1c6            |

test_email : lkay2333+dev2@gmail.com

### pre data

```ts
sourceRecord: {
	source_name: rca
	source_id_: test1002
	email_or_lockeId: E:lkay2333+dev2@gmail.com
}

// auth0 users
app_meatadata {
    hasSourceChecked:{
	    5j47i153ecsr36fmsut62oe1c6: true
    }
}

```

### output
 - [x] should not include `SourceInfo` in token 


## case5

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| lockeId       |   ❌  | users lockeId not existed in DB |
| hasSourceChecked |   ❌  | have checked `hasSourceChecked` before |
| sourceRecord     |   ❌  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 5j47i153ecsr36fmsut62oe1c6            |

test_email : lkay2333+dev3@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {

}

```

### output
 - [x] update `hasSourceChecked`  to `true` 

## case6

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| lockeId       |   ❌  | users lockeId not existed in DB |
| hasSourceChecked |   ✅   | have checked `hasSourceChecked` before |
| sourceRecord     |   ❌  | has `sourceRecord` in DB            |
| client     |   ✅  | rca clients list -> 5j47i153ecsr36fmsut62oe1c6            |

test_email : lkay2333+dev3@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {
	hasSourceCheck: {
		5j47i153ecsr36fmsut62oe1c6: true
	}
}

```

### output
 - [x] should not include `SourceInfo` in token  


## case7

### pre condition 

| Condition        | Status | Description |
|:---------------- |:------:| -----------:|
| endpoint get error       |   ❌  | get error in auth0 side |
| client     |   ✅  | rca clients list -> 5j47i153ecsr36fmsut62oe1c6            |

test_email : lkay2333+dev4@gmail.com

### pre data

```ts
sourceRecord: {

}

// auth0 users
app_meatadata {

}

```

### output
 - [ ] throw error , use can not login in successfully
 - [ ] leave a sceenShot for this one because will cost a long time to deploy older version have error

![[Pasted image 20230703141847.png]]