# PowerAutomate Flow Overview

---

## Flow 1: 
### Recieving Data From Jamf Protect & Sorting Devices Into Jamf School Static Groups

Overview of entire PowerAutomate Flow

<img width="256" src="https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/01.%20Protect%20School%20Connector%20Full.png">



---
### 1. Trigger Block

* Create a `when a HTTP Request is received` block
* Select `Anyone` in the **`who can trigger this flow`** box
* Provide `sample data` from the [Jamf Protect Data Kit](https://www.postman.com/txhaflaire/jamf-open-source-community/collection/fh1725y/jamf-protect-data-kit?action=share&creator=19047489)  postman collection

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/02.%20First%20Trigger%20Block.png)

---
### 2. Filter Out Prevented Threats

* Add a `condition` block
* Set the **`Value`** to `blocked` from the data coming in from the HTTP trigger (aka Jamf Protect)
* Select `is equal to` in the next drop down menu
* Add `true` in the final box

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/03.%20Threat%20Prevention%20Filter.png)

---
### 3. Filter Out Informational Events

* Add a `condition` block to the `false` arm of the previous block
* Set the **`Value`** to `severity` from the data coming in from the HTTP trigger (aka Jamf Protect)
* Select `is equal to` in the next drop down menu
* Add `0` in the final box

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/04.%20Informational%20Filter.png)

---
### 4. GET Devices API call to Jamf School

* Add a `HTTP` block to the `false` arm of the previous block
* In the **`URI`** box set your Jamf School instance URL along with `/api/device?seiralnumber=`
* with your cursor located after the = press the thunderbolt icon to reveal the dynamic objext menu
* Select `serial` from the data coming in from the HTTP trigger (aka Jamf Protect)
* Fill in the relivent settings, including `Authenication Type` to complete the API call (Viewthe [Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) for more information on this)

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/05.%20GET%20Devices%20API.png)

---
### 5. Error Handle API Call

* Add a `condition` block previous block
* Set the **`Value`** to `Status Code` from the data coming in from your Jamf School API Call
* Select `is equal to` in the next drop down menu
* Add `200` in the final box

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/06.%20API%20Call%20Success.png)

---
### 6. Parse JSON Object

* Add a `Parse JSON` block to the `true` arm of the prevouis block
* Provide `sample data` from the **Jamf School API** postman collection by completing a `Get Devices` call in postman and copy/pasting the reponse body into the `sample data` box

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/07.%20Parse%20JSON.png)

---
### 7. Provide a Switch Block

* Add a `switch` block to the previous block
* Set the **`Value`** to `severity` from the data coming in from the HTTP trigger (aka Jamf Protect)

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/08.%20Severity%20Switch.png)

---
### 8. Build Severity Routing

* Add a `switch condition` by clicking on the `+` under the `switch` block
* Set the **`Parameters`** value to `1`

![](https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/09.%20Low%20Switch.png)

---
### 9. Create API Call To Move Device To Static Group

* Add a `HTTP` block to the prevouis switch block
* In the **`URI`** box set your Jamf School instance URL along with `/api/devices/groups/add`
* In the **`Body`** add `{ "groupId": <XXX>, "udids": [ <DYNAMIC VALUE> ] }`
* Replace `<XXX>` with your low severity level group ID in Jamf School
* Replace `<DYNAMIC VALUE>` with `UDID` from the data coming from the parsed JSON data
* Fill in the relivent settings, including `Authenication Type` to complete the API call (Viewthe [Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) for more information on this)

https://github.com/cantscript/JNUC2024/blob/main/Images/No%20Code%20Low%20Code/11.%20Group%20API.png

---
### 10. Build All Severity Routing Options

* Repeat step 8 & 9 replacing the values to match Jamf Protect Severity levels (2 = Mid, 3 = High) and your corresponding Jamf School group IDs


---

## Flow 2: 
### Removing Device From Jamf School Static Group To Enable Flow To Trigger Again

Overview of entire PowerAutomate Flow

INSERT IMAGE


---
### 1. Trigger Block
* Create a `when a HTTP Request is received` block
* Select `Anyone` in the **`who can trigger this flow`** box
* Provide this `sample data` if using the [notification script](https://github.com/cantscript/JNUC2024/blob/main/No-Code%3ALow-Code%20Solutions%20for%20Seamless%20Protection%20With%20Jamf%20/Jamf%20School%20Protect%20workflow.sh) provided in this JNUC example workflow. Else provide your own sample data according to your workflow

`{ "code": 200, "device": { "serialNumber": "ABCDEF123456", "groupId": "123" }}`

INSERT IMAGE

---
### 2. Error Handle Incoming Data

* Add a `condition` block previous block
* Set the **`Value`** to `code` from the data coming in from the script ran on the endpoint
* Select `is equal to` in the next drop down menu
* Add `200` in the final box

INSErT IMAGE

---
### 3. GET Devices API call to Jamf School

* Add a `HTTP` block to the `true` arm of the previous block
* In the **`URI`** box set your Jamf School instance URL along with `/api/device?seiralnumber=`
* with your cursor located after the = press the thunderbolt icon to reveal the dynamic objext menu
* Select `serialNumber` from the data coming in from the HTTP trigger (aka script ran on the EndPoint)
* Fill in the relivent settings, including `Authenication Type` to complete the API call (Viewthe [Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) for more information on this)

INSERT IMAGE

---
### 4. Error Handle API Call

* Add a `condition` block previous block
* Set the **`Value`** to `Status Code` from the data coming in from your Jamf School API Call
* Select `is equal to` in the next drop down menu
* Add `200` in the final box

INSERT IMAGE

---
### 5. Parse JSON Object

* Add a `Parse JSON` block to the `true` arm of the prevouis block
* Provide `sample data` from the **Jamf School API** postman collection by completing a `Get Devices` call in postman and copy/pasting the reponse body into the `sample data` box

INSERT IMAGE

---
### 6. Create API Call To Remove Device To Static Group

* Add a `HTTP` block to the prevouis block
* In the **`URI`** box set your Jamf School instance URL along with `/api/devices/groups/remove`
* In the **`Body`** add `{ "groupId": <GROUP DYNAMIC VALUE>, "udids": [ <DYNAMIC VALUE> ] }`
* Replace `<GROUP DYNAMIC VALUE>` with `groupId` from the orginal trigger
* Replace `<DYNAMIC VALUE>` with `UDID` from the orginal trigger
* Fill in the relivent settings, including `Authenication Type` to complete the API call (Viewthe [Jamf School API Documentation](https://school.jamfcloud.com/api/docs/) for more information on this)

INSERT IMAGE

