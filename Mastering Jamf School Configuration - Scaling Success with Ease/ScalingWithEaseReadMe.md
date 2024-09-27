# Mastering Jamf School Configuration: Scaling Success with Ease!

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/JNUC%202024%20Logo.png" width="512"/>
</p>

---

## Key Moments

Below are a few key slides from the session which might be useful to see when thinking about a deployment strategy

### Manage Objects with Locations

Management Objects such as Config Profiles and Apps can be deloyed in 3 main ways within the concept explained during the session. 

**District Created and Scoped** <br>
Items created and managed at the district level and then scoped from this level. The result is that all devices in all locations will recieve these objects and a location admin will not be able to unscope. Use for essential config but keep very light touch

**District Created and Shared** <br>
Items created and managed at the ditrict level but not scoped. This gives a location admin the ability to scope as they see fit. 

Location admin advantages are that if they are a small team or less confident with managing Apple devices they have approved configuration ready to use which makes thier job easier. 

Advantages for District Admin is if there needs to be a change to this central config it only needs changes once and will filter down to each loction.

**Location Governed** <br>
Iteams created, managed and scoped at the location level by the local IT team / admin. 

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/Mastering%20School%20Config/LocationManagementObject.jpeg" width="512"/>
</p>

### Individual Admin View

From an individual Admins veiw point they only see devices and configurations that belong to their location. All devices and users are imported directly into that location and the admin can create and scope management items that only live at their location. 

The advantage here is that along side these management items they will also get access to any management items made available from the district team and can freely scope these as required (see the horizontal view). As far as the location admin is concerned they have a "full featured" single instance to themselves 

From a district level veiw point (the virtical  view) not only can IT see all devices and users from that location (and all others), quickly move into those locations to aid location admins but also share and / or scope configurations that are essential or recomended for the district to ensure everyone has the same experience or that polices are met. 

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/Mastering%20School%20Config/IndivualAdminView.jpeg" width="512"/>
</p>


### Identity Import Table

In my opinion Identity is key in Jamf School. Its what we can base automation on that allows IT Admins to give any device to any user and them recieve the correct configuration. Not only that, it is repeatable. 

There are four way to import identity data into Jamf School each with their advantages and what I will call "downfalls"

* Authenication
* Syncronisation
* Apple School Manager Sync (with Match)
* Import via CSV/API

In order to get the best results you'll need to use all 4 methods. Below is a table explain what each import method does and doesn't provide

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/Mastering%20School%20Config/IndentityImportsTable.jpeg" width="512"/>
</p>


### Identity Data Flow

Its all well and good knowing which methods do what but you must also know how to import data using each method. 

The key things to remember are
We use Apple School Manager Data for Classroom management tools (Apple Classroom & Jamf Teacher)
We use idP / Directory "user tree structure" for Device Management
We need an authenication method so that a user can attached thier identity to a device (which in turn triggers the automations)

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/Mastering%20School%20Config/IndentityImportFlow.jpeg" width="512"/>
</p>

**School Manager for Classroom Management** <br>
There is a built in integration for syncing with Apple School Manager and its fairly simple. Remember to use the "Match" setting to ensure you append data to the user in Jamf School, rather than create a duplicate user


**Authenication for Device Enrolment** <br>
Jamf School natively supports authenication with 

* Entra
* Google
* LDAPs

For Entra & Google the connection is made via an "Enterprise App" style configuration. For LDAPs Jamf School must be able to communicate with the LDAP server. For more information about Firewall configurations see the [Jamf School Documentation: Firewall Ports, IP Addresses, and URLs Used by Jamf School](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Firewall_Ports_IP_Addresses_and_URLs_Used_by_Jamf_School.html)


**Directory "User Tree" for Device Management** <br>
Jamf School natively supports only LDAPs for Syncronisation. Unlike with Authenications where there are options which enable admins to configure without granting access to on prem servers, this is not possible with Sync. 

Opening up on prem servers to a cloud system can be very problematic to many admins. In this case there are two options to bypass the need for an LDAPs connection. 

1. Create a custom API connector which will pull data from a data source and import into Jamf School
2. Work with a databroker

Most school have a partner that takes data from an SIS, manipulates the data and provisions accounts for other services. Adding a databroker into the mix removes the need for an LDAP connection. 

<p align="center">
<img src="https://github.com/cantscript/JNUC2024/blob/main/Images/Mastering%20School%20Config/IDImportFlowWithDatabroker.jpeg" width="512"/>
</p>


---

## Jamf Marketplace Partners

### "Databrokers"

During the session we mentioned what I refered to as "Databrokers". These are companies whose business it is to manipulate data from one source and provision accounts in other services. 

Using a databroker will limit the stress and interaction with SIS or idP systems when pulling in data for the all important automations. 

Below are 2 such "databrokers" that are listed on our Jamf Marketplace and have Jamf School integrations right out of the box

**Wonde** <br>
*Wonde, simplifies school data management by providing a secure, efficient, and easy-to-use platform. It connects school to over 60 data systems with 600 third-party applications globally to enhance functionality and streamline administrative processes.*

[See More on Jamf Marketplace](https://marketplace.jamf.com/details/wonde-data-sync)


**SalamanderSoft** <br>
*With Integration Provided by our Integration Suite, schools can now automate the management of their users and classes in Jamf School directly from MIS. Saving time for both the users and those tasked with managing their data as well as ensuring that your data is up to date.*

[See More on Jamf Marketplace](https://marketplace.jamf.com/details/salamander-integration-suite)

---


## Resources

Here is a list of addtional sessions delivered by the EMEIA SE team and mainly for the BETT show in the UK. Between the 4 sessions all the concepts covered in this session are covered. 

These resources are great if you want to dig in a little further with the conecpts

[Microsoft, Google & Co: making the most of your identity provider](https://www.youtube.com/watch?v=bTAenuVf9Ng&list=PLlxHm_Px-Ie34WQu_hsfQubqBmjJUQBng&index=7)


[Manage and Secure Apple Devices to Empower End Users](https://www.youtube.com/watch?v=sS2xaKGsyzw&t=18s)


[Jamf School, MDM For Everyone](https://www.youtube.com/watch?v=SMyVUpdBHeI&t=15s)


[Education At Jamf: All Day, Every Day, Any Day](https://www.youtube.com/watch?v=yidxQuC-4S8)

---

## Links

[Jamf School Documentation: Locations](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Locations.html)

[Jamf School Documentation: Device Assignment to Locations](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Device_Assignment_to_Locations.html)

[Jamf School Documentation: Apple School Manager Integration](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Apple_School_Manager_Integration.html#concept-6006)


[Jamf School Documentation: Syncing with an LDAP Directory Service](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Syncing_with_an_LDAP_Directory_Service.html)

[Jamf School Documentation: Microsoft Entra ID Integration](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Microsoft_Azure_Integration.html#ID-0000cc19)

[Jamf School Documentation: Google Sign-In Setup](https://learn.jamf.com/en-US/bundle/jamf-school-documentation/page/Google_Sign-In_Setup.html#ID-0000ce70)
