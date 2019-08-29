+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/2000/1*4oos-kcdjRogDAcDusaYLg.jpeg"
date = "2019-08-21T14:30:30.652Z"
title = "How To Deploy Node.js Functions to Google Cloud."
categories = [ ]
+++




<span class=subtitle>Get Started with Node &amp; GCP</span>


<!--more-->

The serverless trend is the latest evolution of network application architecture. You no longer need to think about the hardware, the OS, or even the running application. Deploy nothing more than the lines of code you need to run wrapped in a node.js function.


Deploying serverless functions to Google’s Cloud Platform (GCP) is not difficult but it requires using and understanding the gcloud command line tool. The gcloudtool enables you to administer your Google Cloud setup via the command line.


Install the gcloud command line tool by downloading the Google Cloud SDK. Make sure the executables are located in your path. Run gcloud --help to make sure it is usable.


## Initializing gcloud


Run gcloud init to set up your environment configuration. gcloud will need a name for the current configuration, enter whatever you want. If you've run this before you'll have the ability to reinitialize, switch configurations, or create a new configuration. Choose whatever is appropriate.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2452/1*USSKHTRtRXnlgqNUUa5uww.png">

You’ll need to log in to your Google account before continuing, gcloud will take care of opening a browser to continue.


After you log in select an existing project or create a new one. Now you’re ready to go!


## Enabling Google Cloud Functions API


Getting started with any of the GCP services requires that you enable the APIs individually. This comes with billing implications so make sure you understand what you enable and what you deploy! For the functions we will deploy there is not much risk but there are services that are deceptively easy to deploy. Some deployments can run you hundreds of dollars in charges even when idle. I’m looking at you Dataflow.


You can turn on the functions API via the web interface or by attempting to do anything with functions via the gcloud tool. Run a command like gcloud functions list to be prompted to turn on API access, enter 'Y' and wait two minutes until you receive a success message.


## Creating a basic http functions


Google cloud functions are handlers in an Express application and you can do anything in them you’d expect to be able to do in an Express app. The basic function signature takes in a request and response object. Sending a response is handled via the response object.


First, initialize your project directory with a package.json. You can use the following command to do this automatically with sensible defaults.

```
$ npm init -y
```

Copy the following JavaScript into an index.js file in your projects directory. This will serve as our function.

```
exports.myFunction = (req, res) => {
  res.send(`<h1>You're awesome 🤘</h1>`);
};
```

## Testing with the functions emulator


Before deploying it’s important to test locally. Deploying takes time and disrupts the development cycle considerably. You can deploy locally with the GCP Functions Emulator.


Before you install: Make sure you are running a supported version of node. As of this writing GCP functions support node versions 6 & 8 with 10 in beta and the cloud functions emulator complains unless you are running node 6 or 8. You can swap between node versions with a tool like nvm. You can still use the functions emulator with other versions of node but the environment differences are on you.


After you switch to the desired node version, install the functions emulator via npm:

```
$ npm install -g @google-cloud/functions-emulator
```

You use the functions emulator the same way you would the gcloud functionsinterface which makes it easy to swap back and forth.


Deploy locally with the following command, subsitute myFunction with whatever you want your function's name to be.

```
functions deploy myFunction --trigger-http
```

We are deploying a basic HTTP function and we need to specify that via the trigger-http flag. You can deploy functions that are triggered via events, PubSub messages, database actions, and more. Check out the full list of triggers via $ gcloud functions event-types list

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/3552/1*vmgbee30RgERU5KEcW9qVw.png">

The functions tool will give you a local URL to view your function, check it out! The functions emulator also provides debugging capabilities so you can troubleshoot your functions in a familiar setting. Read more in the emulator’s documentation.


## Deploying to Google Cloud


Using gcloud to deploy functions is similar to using the functions command line tool except we also need to explicitly specify the runtime, e.g. nodejs8 or nodejs10.

```
$ gcloud functions deploy myFunction --trigger-http --runtime=nodejs8
```

After two minutes you should see a success message and you are ready to go! The success message will also give you the URL for your function so you can visit it immediately.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2292/1*zDTF06kbtNUTmF7Swilrlg.png">

Redeploying functions is as easy as repeating the previous command. Each deployment will update your function.


## Other types of functions


HTTP functions are an obvious first foray into GCP’s functions but you can use cloud functions for a lot more. Look into Google’s Pub/Sub for an extensible way of tying messages into pipelines filled with functions. You can use Google’s Cloud Scheduler to periodically kick off Pub/Sub messages that trigger cloud functions. You can even use Chrome itself inside Google Cloud Functions allowing you to set up an automatic web scraper that dumps results to a database with little more than a handful of GCP services.


Hope this helps get you started! Let me know what you build and what cool ways you tie cloud functions together.


[Share this on Medium](https://medium.com/@jsoverson/how-to-deploy-node-js-functions-to-google-cloud-8bba05e9c10a)
