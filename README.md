# communistar-web

Communistar Web is an exclusive landing page that imports events from akkadu.com and use RSI SDK for interpretation.
This project fetchs events for only a unique user which user id set in the environment variables.

## Test In Preview

The preview urls will vary with the PR number. But the SDK requires a hardcoded origin.
Every time you push something to preview, remember to go to [rsi.akkadu.com](https://rsi.akkadu.com) and change the origin
to your new preview URL. (Credentials in this README)

> https://deploy-preview-`NUMBER`--affectionate-fermi-298ad2.netlify.app/

## Create an event

**Production**
To create a room we need would normally use the Interpreter Manager. But as it is in _construction_ and temporaly can not be used.
We need to directly interact with the _Interpreter SDK_

1. Login in [RSI Dashboard](https://rsi.akkadu.com) and select the key that you want to use. (The one in the `.env` or `default.env`. For
   staging and production check the `netifly.toml` netifly configuration file in this project

2. Create an Event

```bash

POST https://54i2k0z0vf.execute-api.cn-north-1.amazonaws.com.cn/prod/events
Content-Type: application/json
x-sdk-key: KEY
origin: http://localhost:3000

{
  "name": "Comunistar Preview Example",
  "startDate": 1630496799164,
  "endDate": 1630501799164,
  "streamUrl": "https://www.youtube.com/watch?v=WDJKuRsV2fY",
  "streamType": "youtube",
  "floorLanguage": "en-US"
}
```

3. Assign at least one language

```bash
###
PUT https://54i2k0z0vf.execute-api.cn-north-1.amazonaws.com.cn/prod/events/interpreters?roomName=xxwo
Content-Type: application/json
x-sdk-key: KEY
origin: http://localhost:3000

{
  "languageCode": "ko-KR",
  "pair1": "abelbordonado@gmail.com",
  "pair2": "abel-1@akkadu-team.com"
}
```

4. Communistar Keys are special because Communistar can subscribe to floor. Find the new created key in Dynamo DB and add the config for it. We require add the key `allowSubscribeFloor` inside the config object of the key (You can add the config object if there is any)

```json
 "config": {
  "allowSubscribeFloor": true
 },
```

6. After the creation, the event shall be visible in [RSI Dashboard](https://rsi.akkadu.com).

7. Accessing to [Akkadu Dashboard](https://akkadu.com) You shall be able to edit the event properties.

:warning: You can create an event from [Akkadu Dashboard](https://akkadu.com), but you will need to access DynamoDB manually and add the `roomName` to the `sdkKey`.

**Staging and Localhost**

As the `SDK Module` only works with production, we need to create room names that match the production room names`.

1. Login in a preview or localhost version of akkadu. Create an event in the account of the user of staging.

2. Use the Akkadu API to change the `roomName` and match the one created in production.

```bash

###
PUT https://devapi.akkadu.com/v2/users/USER_ID/events/EVENT_ID
authorization: Bearer TOKEN

{
   "roomName": "xxwo",
   "id": EVENT_ID
}
```

If the room name is not the same of an existing event in production, the information will load but the SDK will fail.
At the same time, to test the audio we need to use the production event, while the event data (name, poster) will depend from the staging event.

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

### Crednetials

Netifly: akkadutech@gmail.com (akkadu_team_1234)

Stagin Akkadu communistar@akkadu-team.com (akkadu_team_1234)

Akkadu.com communistar@akkadu-team.com (akkadu_team_1234)

RSI Dashboard communistar@akkadu-team.com (akkadu_team_1234)

Domain: rsistar.com

https://www.cafe24.com/ ID: shedu28 PW: shshsh48
# test
