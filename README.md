# Zoom Webhook Sample Node.js

Use of this sample app is subject to our [Terms of Use](https://zoom.us/docs/en-us/zoom_api_license_and_tou.html).

This is a Node.js / Express server that receives [Zoom Platform Webhooks](https://marketplace.zoom.us/docs/api-reference/webhook-reference) and [Zoom Video SDK Webhooks](https://marketplace.zoom.us/docs/api-reference/webhook-reference/video-sdk-events) .

If you would like to skip these steps and just deploy the finished code to Heroku, click the Deploy to Heroku button. (You will still need to configure a few simple things, so skip to [Deployment](#deployment).)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Installation

In terminal, run the following command to clone the repo:

`$ git clone https://github.com/zoom/webhook-sample-node.js.git`

## Setup

1. In terminal, cd into the cloned repo:

   `$ cd webhook-sample-node.js`

1. Then install the dependencies:

   `$ npm install`

1. Create an environment file to store your Video SDK Apps's Key and Secret:

   `$ touch .env`

1. Add the following code to the .env file, and insert your Webhook Verification Token found on the Features page in the Zoom App Marketplace:

   ```
   ZOOM_WEBHOOK_VERIFICATION_TOKEN=ZOOM_WEBHOOK_VERIFICATION_TOKEN_HERE
   ```

   ![Zoom Webhook Verification Token](https://marketplace.zoom.us/docs/images/migrated/1635884356131.png "Zoom Webhook Verification Token")

1. Save and close .env.

1. Start the server:

   `$ npm run start`

1. We need to expose the local server to the internet to accept post requests, we will use [Ngrok](https://ngrok.com) (free) for this.

   Once installed, open a new terminal tab and run:

   `$ ngrok http 4000`

   > NOTE: [I've put ngrok in my PATH so I can call it globally.](https://stackoverflow.com/a/36759493/6592510)

1. Copy the ngrok https url displayed in terminal. In your apps Event notification endpoint URL input, paste your ngrok https url. Remember to include `/webhook` path.

   Example: `https://abc123.ngrok.io/webhook`

   ![Zoom Webhook Configuration](https://marketplace.zoom.us/docs/images/migrated/1635885688814.png "Zoom Webhook Configuration")

1. Choose the events you'd like to subscribe to.

   ![Zoom Webhook Events](https://marketplace.zoom.us/docs/images/migrated/1635884395709.png "Zoom Webhook Events")

1. Click "Save".

## Usage

1. Trigger the respective Webhook.

   For example, if you chose the [Start Meeting Webhook](https://marketplace.zoom.us/docs/api-reference/webhook-reference/meeting-events/meeting-started), start a Zoom Meeting. You will see the Webhook headers and payload logged in terminal.

   ```js
   {
     'host': 'abc123.ngrok.io',
     'user-agent': 'Zoom Marketplace/1.0a',
     'content-length': '335',
     'authorization': '{webhook_verification_token}',
     'clientid': '{client_id}',
     'content-type': 'application/json; charset=utf-8',
     'x-forwarded-for': '{x_forwarded_for}',
     'x-forwarded-proto': 'https',
     'x-zm-trackingid': '{x_zm-trackingid}',
     'accept-encoding': 'gzip'
   }
   ```

   ```js
   {
     event: 'meeting.started',
     payload: {
       account_id: '{account_id}',
       object: {
         duration: 0,
         start_time: '2021-11-02T20:43:19Z',
         timezone: 'America/Denver',
         topic: "{topic}",
         id: '{meeting_id}',
         type: 4,
         uuid: '{meeting_uuid}',
         host_id: '{host_user_id}'
       }
     },
     event_ts: 1635885799302
   }
   ```

## Deployment

### Heroku

If you used the "Deploy to Heroku" button, fill in the blanks.

1. Enter a name for your app on the page the button took you to (or leave it blank to have a name generated for you), and fill in the values for these:

   - `ZOOM_WEBHOOK_VERIFICATION_TOKEN` (Your Zoom Webhook Verification Token, found on your App's Features page)

1. Then click "Deploy App".

1. Now you can use your deployed url Heroku provides as the Event notification endpoint URL. Copy the Heroku https url from the "View" button. In your apps Event notification endpoint URL input, paste your Heroku https url. Remember to include `/webhook` path.

   Example: `https://abc123.herokuapp.com/webhook`

If you cloned this repo, use the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) to deploy your server.

1. In terminal, create a Heroku app:

   `$ heroku create`

1. Add your files:

   `$ git add -A`

1. Commit your files:

   `$ git commit -m "deploying to heroku"`

1. Deploy your server by pushing your files to Heroku:

   `$ git push origin heroku`

1. Navigate to your app on the Heroku dashboard, click settings, and add your App's Webhook Verification Token in the Config Variables:

   - `ZOOM_WEBHOOK_VERIFICATION_TOKEN` (Your Zoom Webhook Verification Token, found on your App's Features page)

1. Now you can use your deployed url Heroku provides as the Event notification endpoint URL. Copy the Heroku https url displayed in terminal. In your apps Event notification endpoint URL input, paste your Heroku https url. Remember to include `/webhook` path.

   Example: `https://abc123.herokuapp.com/webhook`

### Other Server Hosting

For Other Server Hosting information, see [this tutorial](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/deployment#choosing_a_hosting_provider).

## Need help?

If you're looking for help, try [Developer Support](https://devsupport.zoom.us)   or our [Developer Forum](https://devforum.zoom.us). Priority support is also available with [Premier Developer Support](https://zoom.us/docs/en-us/developer-support-plans.html) plans.
