# template-wedding
A template for simple, yet functioning Wedding Event website.

Originally this was a private repo for my own wedding, and I have decided to open up this repo containing the essentials to creating your own version.
The project uses Vite + React with Material UI for the UI components.
The backend and CI/CD was originally deployed using AWS, but your preferred hosting solution should work.

## Features
* Passcode Login page authenticated using a Lambda Function URL (written in Python) + JWT session token
* RSVP form (using Formik) tied to a Lambda Function URL (again, written in Python) + DynamoDB table + SNS Email Notifications
* Clean, simple MUI template tweaked from MUI's own OnePirate template and MUI examples
* Google Maps API for display the wedding location

## Build locally
1. Fork this repo, then clone it locally.
2. Install the packages ```npm i```
3. Run the development server ```npm run dev```
4. Open http://localhost:5000/ in your favourite browser

## Test
Who needs tests?

## Infrastructure (on AWS)
### Amplify
I used Amplify to host and deploy the wesbite.
This means you can link your GH repo to your Amplify project in the AWS Console, so that on push it redeploys.
Amplify also allows branched deployment, such that you could have a development and production deployments.
You can purchase a domain name through AWS Route 53, or any domain provider.
This project uses Vite for bundling the Javascript, so be sure the Amplify build script is using Vite's correct commands.

### Lambda
I used Lambdas to handle authentication and handle RSVPs.
The code was written in Python and deployed manually using the AWS SAM CLI (i.e. not part of the Amplify CI/CD pipeline).

### DynamoDB
I used DynamoDB to track guest RSVPs.
I manually created a DynamoDB table (with default settings) in the AWS Console and pointed the Lambdas to it (using boto3's DynamoDB client).

### SNS Email Notifications
I setup Email Notification using SNS and used boto3's SNS client to trigger email notifications to my personal email after each guest's RSVP.
*Note*: SMS Notifications cost money (luckily capped at $1/month by default) so I would recommend using emails.

## Deploy
Once CI/CD is setup with Amplify, it should be as easy as pushing code and watching your website redeploy live.

## Cost
Be sure to check AWS pricing for all services (at time of writing, all services are free tier eligible), but other than the domain name (~$15/year) my costs for running this setup were under $1/month (on-going Route 53 costs, and a few SNS Text Notification mistakes on my part).

## Contributing
I won't be looking at any PRs or Issues raised. Feel free to fork and improve at your leisure!
