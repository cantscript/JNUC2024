# No-Code:Low-Code Solutions for Seamless Protection With Jamf School & Jamf Protect

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/JNUC%202024%20Logo.png" width="512"/>
</p>

---

## I Have a Confession.....

I'll hold my hands up, during the session I was a **little misleading** and make the workflow a *little more difficult*. 

This was done with the best intensions as I wanted to show you the power of both making an API call and receiving data from a second source with an No Code, Low Code platform. As there will be times that this is absolutely the action you will need to take.

However, in the session I explained that Jamf Protect **only** gave the device `Serial Number`, which is why we had to reach out to Jamf School and revieve more data to retrive the `UDID`

Although Jamf Protect does send the `Serial Number`, it does, in fact, **also** provide the `UDID` of the device! 

If you decide to create a workflow in your environment you can simplfy your flow if all you need is the UDID, but if you need more data you now know how to put those steps together. 

Your welcome ;-) 

## Session Demo Workflow

For the session we run through a demo workflow that provided the user with a custom notification when the endpoint triggers a Jamf Protect Event

### Outcome

The outcome of the workflow is as follows. Present the user with a custom notification (using swiftDialog) when endpoint triggers a Jamf Protect Alert. 

The notification must be different for a low, medium and high severity event. 

We also do not want to trigger a custom notfication if Jamf Protect has automatically prevented the event via Threat Prevention (Project triggers its own notification) or if the event is an informational event (to prevent too many notifications and becoming a problem for the user)


<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/Example%20Flow%20Outcome.jpeg" width="512"/>
</p>


### The Flow Logic

In order for this flow to work we must step through the flow and manage the data. The flow steps are as follows

1. PowerAutomate recieves data from Jamf Protect
2. Filter out any events that have been automatically prevented by Jamf Protect
3. Filter out any events that are informationally only
4. Apply some data manipulation and logic in PowerAutomate
5. PowerAutomate to prepare and make an API call to Jamf School to add a device to a group
6. Jamf School to perform an action / start a workflow on endpoint to display notfication 

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/Example%20Flow%20Logic.jpeg" width="512"/>
</p>

### The Puzzle Pieces

There are four major steps to the flow

1. Device triggers Jamf Protect Alert
2. Jamf Protect sends data to PowerAutomate
3. PowerAutomate sends API to Jamf School
4. Jamf School triggers action on Device

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/Example%20Flow%20Elements.jpeg" width="512"/>
</p>

## Real World Example

As noted in the session the demo workflow performed in of itself isn't actaully doing anything to further protect the device. These actions, showing user notifications, are simply an easy way of showing soemthing different happening depending on the severity level

However the important take away from the session was not the actions I performed but the workflow, the method, using a No Code, Low Code platflorm. 

A real world set of actions an admin might take to further protect devices in a seemless and automated way for a high severity event, are

1. Add or Remove configuration from the device. Adding or removing porfiles to either further lock down the device funcationality or removing access from resources
2. Trigger the installation and run the Incident Response tool, Aftermath, in order to collect logs and data prior to the even happening to further analyse or indentify compromise
3. Look the users 0365 account and log them out of any active sessions to prevent further access in the event of compromise
4. Send a teams / slack / email message to the IT department with the users and device details so that IT can proactively help the user

ADD SCREEN SHOT

---

## No Code, Low Code Platform

Although PowerAutomate was the No Code, Low Code Platform that we used in the session, this type of workflow can be achieved with other No Code, Low Code platforms. Other examples of No Code, Low Code Platforms are

* Okta Workflows
* Torq
* If This Then That
* make.com
* Tines

Before committing to a platform you should first evaluate the features and any costs linked which such a platform. 

A View of the PowerAutomate workflow created for this session can be seen in detail here - [PowerAutomate Flow Overview](https://github.com/cantscript/JNUC2024/blob/main/No-Code%3ALow-Code%20Solutions%20for%20Seamless%20Protection%20With%20Jamf%20/PowerAutomate%20Flow%20Overview.md)

---

## Tools

During the session I used a number of tools

### JamfCheck

<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/JamfCheckIcon.png" width="128"/>

The "JamfCheck" is a Apple code-signed and notarized macOS app that allows you to easily run a couple of check's for Jamf Pro, Jamf Connect and Jamf Protect in a single app.

[Get JamfCheck](https://github.com/txhaflaire/JamfCheck)

---

### Postman

<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/PostmanIcon.png" width="128"/>

Postman is an API platform for building and using APIs. Its great for testing API's for workflows and understanding what data needs to be send or how data is recieved

[Get Postman](https://www.postman.com)

---

### CodeRunner

<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/CodeRunnerIcon.png" width="128"/>

CodeRunner was designed to support all of the most widely used programming languages and run them instantly.

During this session I showed scripts in CodeRunner all you need as a text editor altough something designed for code syntex is recommeneded. Another example would be BBEdit

[Get CodeRunner](https://coderunnerapp.com)

---

## Resources

During this session I used a number of Postman collections and example scripts

### Jamf Protect Data Kit

This collection contains an extensive array of sample events, which can be transmitted individually or in bulk to a Security Information and Event Management (SIEM) solution or any HTTP receiver or sent to a Microsoft Sentinel workspace.

[Get Jamf Protect Data Kit Postman Collection](https://www.postman.com/txhaflaire/jamf-open-source-community/collection/fh1725y/jamf-protect-data-kit?action=share&creator=19047489)

---

### Jamf School API Collection

This collection cantains all endpoints listed in the Jamf School API documentation along with a number of generic examples where the API call requires a body

To use the collection import <br>
[Jamf School API Collection](https://github.com/cantscript/JNUC2024/blob/main/No-Code%3ALow-Code%20Solutions%20for%20Seamless%20Protection%20With%20Jamf%20/Jamf%20School%20API.postman_collection.json) <br>
[Jamf School Environment Template](https://github.com/cantscript/JNUC2024/blob/main/No-Code%3ALow-Code%20Solutions%20for%20Seamless%20Protection%20With%20Jamf%20/Jamf%20School%20API%20Enivironment%20Template.postman_environment.json)

Once the Jamf School Environmnet Template has been imported to Postman the minimum you need to fill out is <br>
`username` <br>
`password` <br>
`baseurl`

`baseurl` must include `/api` for example `https://myinstance/jamfcloud.com/api`

---

### Example swiftDialog Script

During the session we created an example workflow which shows a custom notification on an enduser device depending on the severity level of an event triggered. 

The example script shows 3 different notifications and then triggers the second PowerAutomate flow which removes the device from the static group in Jamf School

[Get Example swiftDialog Script](https://github.com/cantscript/JNUC2024/blob/main/No-Code%3ALow-Code%20Solutions%20for%20Seamless%20Protection%20With%20Jamf%20/Jamf%20School%20Protect%20workflow.sh)


<img src="https://github.com/swiftDialog/swiftDialog/blob/main/dialog/Assets.xcassets/AppIcon.appiconset/swiftDialog_128.png" width="128"/>


The script requires that swiftDialog is installed on the end user device prior to running

[Get swiftDialog](https://github.com/swiftDialog/swiftDialog)

---

### Aftermath

<img src="https://github.com/jamf/aftermath/blob/main/AftermathLogo.png" width="256"/>

At the end of the session I gave a real world example of actions that you could take to keep your devices protected. 

As part of that example I mentioned a tool called Aftermath.

Aftermath can be leveraged by defenders in order to collect and subsequently analyze the data from the compromised host. Aftermath can be deployed from an MDM (ideally), but it can also run independently from the infected user's command line.

[Get Aftermath](https://github.com/jamf/aftermath?tab=readme-ov-file)

## Links

Links to documentation to support this session

[Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) <br>
[Using Jamf Protect Cloud for Alerts and Data Forwarding](https://learn.jamf.com/en-US/bundle/jamf-protect-documentation/page/Creating_an_Action_Configuration.html#ariaid-title7)