# No-Code:Low-Code Solutions for Seamless Protection With Jamf School & Jamf Protect

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/JNUC%202024%20Logo.png" width="512"/>
</p>

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

## Links

Links to documentation to support this session

[Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) <br>
[Using Jamf Protect Cloud for Alerts and Data Forwarding](https://learn.jamf.com/en-US/bundle/jamf-protect-documentation/page/Creating_an_Action_Configuration.html#ariaid-title7)