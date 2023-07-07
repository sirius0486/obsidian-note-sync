### login url

> dev:  

```js
https://settings-prod.locke-dev.rea-group.com/api/authenticate?redirect_path=%2Fglobal-sign-out%3Fclient_id%3D7fj1shu31fnrbgf8at0olfhm9q%26redirect_uri%3Dhttps%3A%2F%2Flocke-demo-prod.locke-dev.rea-group.com%2Fprofile



rea: 3b13kuk1s7s18c5olh3t3o2jmt
rca: 2i429vaqutmpits0itbluc4fh3

prod:
rea:   1slo5q0g99ss1e5cfctkdj3ni6, 63b4th825kkloal0u0b677vahs
rca:  1p48kcl0ftem2iee52ih34034, 5j47i153ecsr36fmsut62oe1c6


// lk admin au 
2g19j074kivp4pd8rrteu6fdep:8na3aeov5tik95m9p2hrn72up3lfek7ec9443tp1rj9jua0q732

// prod   clientId:clientSecret after base64 encode
MmcxOWowNzRraXZwNHBkOHJydGV1NmZkZXA6OG5hM2Flb3Y1dGlrOTVtOXAyaHJuNzJ1cDNsZmVrN2VjOTQ0M3RwMXJqOWp1YTBxNzMy

test-dev-02 rca E:lkay2333+dev2@gmail.com
test-dev-01 rca L: generated_locked_id

lkay2333+dev2@gmail.com

https://id-dev.realestate.com.au/authorize?client_id=112lqg4crpvoi8a2nkr9de9lf7&response_type=code&audience=default&scope=openid+profile+email+phone+offline_access&redirect_uri=https%3A%2F%2Flocke-demo.locke-dev.rea-group.com%2Fauth%2Fcallback&connection=email


https://id-dev.realestate.com.au/authorize?client_id=3b13kuk1s7s18c5olh3t3o2jmt&response_type=code&audience=default&scope=openid+profile+email+phone+offline_access&redirect_uri=https%3A%2F%2Flocke-demo.locke-dev.rea-group.com%2Fauth%2Fcallback&connection=email
```

![[Pasted image 20230703144634.png]]

![[Pasted image 20230704141411.png]]
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

'hQW11zQer3bjwcqk5ZxBRzZDTRgqEBt8'  // default client in locke_demo dev
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
	email_or_lockeId: L:generated_new_one
}

// auth0 users app_metadata
app_meatadata {
	lockeId: generated_new_one,
}

// use admin-api create user to create a new user in auth0 *need VPN connected*
curl -i -X POST "https://admin-management-api.locke-dev.rea-group.com/user" -H "accept: */*" -H "Authorization: Basic aFFXMTF6UWVyM2Jqd2NxazVaeEJSelpEVFJncUVCdDg6cDZMQW9haklwSThoN1c2RllNcC13amhHMlRnNkpCQkozQ3ZpdHo5ektXeFlPcEctU3BsamV2bThsbEZYdm10Vw==" -H "Content-Type: application/json" -d "{\"email\":\"lkay2333+dev1@gmail.com\"}"

```

### output
 - [x] updated sourceInfo in token  
	 -  `custom: source_name : test-dev-01 
	 -  `custom: source_name: rca`      in   **profile page** after login  
 - [x] set `sourceChecked` like     `app_meatadata { clentID: true }`   auth0
 

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
	    clientId: true
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
	source_id_: test-dev-02
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
 - [x] should not include source info in token

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
 - [x] throw error , use can not login in successfully






### global sign out


### dev

```js

https://admin-management-api.locke-dev.rea-group.com/user/global-logout


$ echo -n "<client_id>:<client_secret>" | bash64 -w 0

hQW11zQer3bjwcqk5ZxBRzZDTRgqEBt8:p6LAoajIpI8h7W6FYMp-wjhG2Tg6JBBJ3Cvitz9zKWxYOpG-Spljevm8llFXvmtW

curl -i -X POST "https://admin-management-api.locke-dev.rea-group.com/user/global-logout" -H "accept: */*" -H "Authorization: Basic aFFXMTF6UWVyM2Jqd2NxazVaeEJSelpEVFJncUVCdDg6cDZMQW9haklwSThoN1c2RllNcC13amhHMlRnNkpCQkozQ3ZpdHo5ektXeFlPcEctU3BsamV2bThsbEZYdm10Vw==" -H "Content-Type: application/json" -d "{\"email\":\"lkay2333@gmail.com\"}"

```

1. confirm   -> no problem -> deploy to dev
2. test   , call admin-api in auth0 ,   check log in cloud watch   cognito whether logout


### prod

```js

https://api.id.realestate.com.au/admin/user/global-logout


$ echo -n "<client_id>:<client_secret>" | bash64 -w 0



curl -i -X POST "https://api.id.realestate.com.au/admin/user/global-logout" -H "accept: */*" -H "Authorization: Basic <clientId:clientSecret>" -H "Content-Type: application/json" -d "{\"email\":\"lkay2333@gmail.com\"}"

```








## global sign out

### src/auth0EventsHandler/globalSignOutEventHandler.ts
```ts
import { GlobalSignOutEventData } from '../utils/types';
import { getGlobalSignOutUser, globalSignOutUser } from "../services/globalSignOutService";
import { logger } from '@locke/locke-logger-module';
import { operationErrorHandler } from "../services/errorService";

export const globalSignOutEventHandler = async (data: GlobalSignOutEventData, sequenceNumber: string) => {
  const user = await getGlobalSignOutUser( data.username );
  if (user) {
    await globalSignOutUser(data.username, sequenceNumber);
    logger.info(`Finish global sign out user with username: ${ data.username }`);
  } else {
    await operationErrorHandler('Global sign out User not found', `User not found for global sign out in Cognito with username: ${ data.username }`, { sequenceNumber });
    logger.info(`Global sign out User not found with username ${ data.username }`);
  }
};
```

### src/services/globalSignOutService.ts
```ts
import { logger } from '@locke/locke-logger-module';
import config from '../utils/config';
import { CognitoClient } from '../clients/cognitoClient';
import { LOCKE_USER_POOL_TABLE } from "../utils/constants";
import { operationErrorHandler } from './errorService';

const getCommonParams = (lockeId: string) => ({
  UserPoolId: config.userpoolID,
  Username: lockeId
});
export const globalSignOutUser = async (lockeId: string, sequenceNumber: string) => {
  try {
    await new CognitoClient().adminUserGlobalSignOut(getCommonParams(lockeId));
    logger.info(`Success global sign out user by ${ lockeId } from cognito user pool ${ config.userpoolID }`);
  } catch (error) {
    await operationErrorHandler(error, `Got error when global sign out user by ${ lockeId } from cognito user pool`, { sequenceNumber });
  }
};

export const getGlobalSignOutUser = async (lockeId: string) => {
  try {
    return await new CognitoClient().adminGetUser(getCommonParams(lockeId));
  } catch (error) {
    await operationErrorHandler(error, `Failed to get user with locke_id ${ lockeId } from ${ LOCKE_USER_POOL_TABLE }`);
    return;
  }
};


```


### test/auth0EventsHandler/handler.test.ts
```ts
import { EventType } from '@locke/locke-events-sdk';
import { userSignUpEventHandler } from '../../src/auth0EventsHandler/userSignUpEventHandler';
import { updateEmailEventHandler } from '../../src/auth0EventsHandler/updateEmailEventHandler';
import { phoneNumberUpdateEventHandler } from '../../src/auth0EventsHandler/phoneNumberUpdateEventHandler';
import { deleteUserEventHandler } from '../../src/auth0EventsHandler/deleteUserEventHandler';
import { globalSignOutEventHandler } from '../../src/auth0EventsHandler/globalSignOutEventHandler';
import { handleAuth0UserEvent } from '../../src/auth0EventsHandler/handler';
import {
  DeleteUserEventData,
  LockeEvent,
  SignupEventData,
  UpdateEmailEventData,
  UpdatePhoneNumberEventData,
  GlobalSignOutEventData
} from '../../src/utils/types';

jest.mock('../../src/auth0EventsHandler/updateEmailEventHandler');
jest.mock('../../src/auth0EventsHandler/userSignUpEventHandler');
jest.mock('../../src/auth0EventsHandler/phoneNumberUpdateEventHandler');
jest.mock('../../src/auth0EventsHandler/deleteUserEventHandler');
jest.mock('../../src/auth0EventsHandler/globalSignOutEventHandler');

describe('handleAuth0UserEvent',  () => {
  beforeEach(() => {
    (userSignUpEventHandler as jest.Mock).mockResolvedValue({});
    (updateEmailEventHandler as jest.Mock).mockResolvedValue({});
    (phoneNumberUpdateEventHandler as jest.Mock).mockResolvedValue({});
    (deleteUserEventHandler as jest.Mock).mockResolvedValue({});
    (globalSignOutEventHandler as jest.Mock).mockResolvedValue({});
  });

  afterEach(jest.resetAllMocks);

  it('should call userSignUpEventHandler and transform data when event type is User_Signup ', () => {
    const data = {
      clientID: 'clientID',
      triggerSource: 'PostConfirmation_ConfirmSignUp',
      phoneNumber: '+8612345'
    } as unknown as SignupEventData;
    const payload = {
      cloudEventsVersion: '1',
      eventType: EventType.User_Signup,
      data,
    } as unknown as LockeEvent;

    handleAuth0UserEvent(payload, 'sequenceNumber');
    expect(userSignUpEventHandler).toBeCalledWith(data, 'sequenceNumber');
  });

  it('should call updateEmailEventHandler and transform data when event type is Update_Email ', () => {
    const data = {
      clientID: 'clientID',
      newEmail: 'newemail@gmail.com'
    } as unknown as UpdateEmailEventData;
    const payload = {
      eventType: EventType.Update_Email,
      data,
    } as unknown as LockeEvent;

    handleAuth0UserEvent(payload, 'sequenceNumber');
    expect(updateEmailEventHandler).toBeCalledWith(data, 'sequenceNumber');
  });

  it('should call phoneNumberUpdateEventHandler and transform data when event type is  Update_Phone_Number', () => {
    const data = {
      clientID: 'clientID',
      phoneNumber: '+8612345'
    } as unknown as UpdatePhoneNumberEventData;
    const payload = {
      eventType: EventType.Update_Phone_Number,
      data,
    } as unknown as LockeEvent;

    handleAuth0UserEvent(payload, 'sequenceNumber');
    expect(phoneNumberUpdateEventHandler).toBeCalledWith(data, 'sequenceNumber');
  });

  it('should call deleteUserEventHandler and transform data when event type is Delete_User', () => {
    const data = {
      clientID: 'clientID',
      username: 'fake-locke-id'
    } as unknown as DeleteUserEventData;
    const payload = {
      eventType: EventType.Delete_User,
      data,
    } as unknown as LockeEvent;

    handleAuth0UserEvent(payload, 'sequenceNumber');
    expect(deleteUserEventHandler).toBeCalledWith(data, 'sequenceNumber');
  });

  it('should call globalSignOutEventHandler and transform data when event type is Global_Sign_Out', () => {
    const data = {
      clientID: 'clientID',
      username: 'fake-locke-id'
    } as unknown as GlobalSignOutEventData;
    const payload = {
      eventType: EventType.Global_Sign_Out,
      data,
    } as unknown as LockeEvent;

    handleAuth0UserEvent(payload, 'sequenceNumber');
    expect(globalSignOutEventHandler).toBeCalledWith(data, 'sequenceNumber');
  });
});

```

### test/auth0EventsHandler/globalSignOutEventHandler.test.ts
```ts
import { globalSignOutUser, getGlobalSignOutUser } from '../../src/services/globalSignOutService';
import { globalSignOutEventHandler } from '../../src/auth0EventsHandler/globalSignOutEventHandler';
import { GlobalSignOutEventData } from '../../src/utils/types';
import { operationErrorHandler } from "../../src/services/errorService";

jest.mock('../../src/services/globalSignOutService');
jest.mock('../../src/services/errorService');

describe('globalSignOutEventHandler', () => {
  const mockOperationErrorHandler = jest.fn();

  it('should call global sign out user in cognito', async () => {
    (getGlobalSignOutUser as jest.Mock).mockResolvedValue('user');
    const data = {
      username: 'test-username'
    } as unknown as GlobalSignOutEventData;
    await globalSignOutEventHandler(data, 'sequence-number');

    expect(getGlobalSignOutUser).toHaveBeenCalledWith( 'test-username');
    expect(globalSignOutUser).toHaveBeenCalledWith('test-username', 'sequence-number');
  });

  it('should log error user info and put metric when user failed to global sign out in cognito', async () => {
    (operationErrorHandler as jest.Mock).mockImplementation(mockOperationErrorHandler);

    const data = {
      username: 'test-username'
    } as unknown as GlobalSignOutEventData;
    await globalSignOutEventHandler(data, 'sequenceNumber');

    expect(getGlobalSignOutUser).toHaveBeenCalledWith('test-username');
    expect(operationErrorHandler).toHaveBeenCalledWith(
      'Global sign out User not found', `User not found for global sign out in Cognito with username: ${ data.username }`, { sequenceNumber: 'sequenceNumber'});
  });
});

```

### test/clients/cognitoClient.test.ts
```ts
import { CognitoClient } from '../../src/clients/cognitoClient';
import {
  CognitoIdentityProviderClient,
  AdminCreateUserCommand,
  AdminSetUserPasswordCommand,
  AdminUpdateUserAttributesCommand,
  AdminGetUserCommand,
  AdminDeleteUserCommand,
  AdminUserGlobalSignOutCommand
} from '@aws-sdk/client-cognito-identity-provider';

jest.mock('@aws-sdk/client-cognito-identity-provider');

describe('CognitoClient', () => {
  beforeEach(() => {
    const mockSend = jest.fn(() => ({ promise: jest.fn() }));
    (CognitoIdentityProviderClient as unknown as jest.Mock).mockImplementation(() => ({
      send: mockSend
    }));
  });
  afterEach(jest.clearAllMocks);

  it('should create user', async () => {
    (AdminCreateUserCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id'
    };
    await new CognitoClient().adminCreateUser(params);

    expect(AdminCreateUserCommand).toHaveBeenCalledWith(params);
  });

  it('should call set password', async () => {
    (AdminSetUserPasswordCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id',
      Password: 'password',
      Permanent: true
    };
    await new CognitoClient().adminSetPassword(params);

    expect(AdminSetUserPasswordCommand).toHaveBeenCalledWith(params);
  });

  it('should call update user', async () => {
    (AdminUpdateUserAttributesCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id',
      UserAttributes: [],
    };
    await new CognitoClient().adminUpdateUser(params);

    expect(AdminUpdateUserAttributesCommand).toHaveBeenCalledWith(params);
  });

  it('should call get user', async () => {
    (AdminGetUserCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id',
    };
    await new CognitoClient().adminGetUser(params);

    expect(AdminGetUserCommand).toHaveBeenCalledWith(params);
  });

  it('should call delete user', async () => {
    (AdminDeleteUserCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id',
    };
    await new CognitoClient().adminDeleteUser(params);

    expect(AdminDeleteUserCommand).toHaveBeenCalledWith(params);
  });

  it('should call global sign out user', async () => {
    (AdminUserGlobalSignOutCommand as unknown as jest.Mock).mockImplementation(jest.fn);
    const params = {
      UserPoolId: 'fake-userpool-id',
      Username: 'fake-locke-id',
    };
    await new CognitoClient().adminUserGlobalSignOut(params);

    expect(AdminUserGlobalSignOutCommand).toHaveBeenCalledWith(params);
  });
});

```


### test/services/globalSignOutService.test.ts
```ts
import { CognitoClient } from '../../src/clients/cognitoClient';
import { operationErrorHandler } from '../../src/services/errorService';
import { globalSignOutUser } from '../../src/services/globalSignOutService';
import { CognitoUser } from "../../src/services/cognitoUserService";
import { logger } from '@locke/locke-logger-module';
import config from "../../src/utils/config";

jest.mock('@locke/locke-logger-module');
jest.mock('../../src/services/metricService');
jest.mock('../../src/clients/cognitoClient');
jest.mock('../../src/services/errorService');
describe('globalSignOutService', () => {
  const mockGlobalSignOut = jest.fn();
  const mockOperationErrorHandler = jest.fn();

  beforeEach(() => {
    (CognitoClient as jest.Mock).mockImplementation(() => ({
      adminUserGlobalSignOut: mockGlobalSignOut,
    }));
    (operationErrorHandler as jest.Mock).mockImplementation(mockOperationErrorHandler);
  });
  afterEach(jest.clearAllMocks);

  it('should call cognito client to global sign up user', async () => {
    const user = {
      email: 'test@gmail.com',
      locke_id: 'locke_id',
    } as unknown as CognitoUser;

    await globalSignOutUser(user.locke_id, 'sequenceNumber');

    expect(logger.info).toHaveBeenCalledWith(`Success global sign out user by ${ user.locke_id } from cognito userpool ${ config.userpoolID }`);
    expect(mockGlobalSignOut).toHaveBeenCalledWith({
      UserPoolId: config.userpoolID,
      Username: user.locke_id,
    });

  });

  it('should log the error message and call putOperationErrorMetricData', async () => {
    (mockGlobalSignOut as jest.Mock).mockRejectedValue('error');
    const user = {
      email: 'test@gmail.com',
      locke_id: 'locke_id',
    } as unknown as CognitoUser;

    await globalSignOutUser(user.locke_id, 'sequenceNumber');

    expect(operationErrorHandler).toHaveBeenCalledWith(
      'error', `Got error when global sign out user by ${ user.locke_id } from cognito userpool`, { sequenceNumber: 'sequenceNumber'});
  });
});

```