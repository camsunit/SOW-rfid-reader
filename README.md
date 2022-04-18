# Statement of Work - Attendance System using RFID

A document prepared by 
LogicBots on 18th April 2022

## Table of Content

* Executive Summary
* Delivery Scope
* Device APIs
* Devices
* Maintenance
* Exclusions
* Deliverables
* Investment and Cost
* Customer Responsibilities
* Acceptance Criteria
* Assumptions


## Executive Summary
This documentation is to serve as a 'Statement of Work' or SOW for developing an RFID based smart attendance system to enhance and empower Administration. The advancement in the field of IoT, Networks, Computing and Data Science has made possible Integrated systems that can help business. Such a system would include a means to capture, catalogue and analyze data, along with tools to enforce 'business logic'.

LogicBots will work with Mr Pandian to:

* Develop RFID Reader functionality.
* Develop Attendance Mode functionality. 
* Develop host software for displaying the esp32 serial content.
* Develop device access page for system configuration.
* Managing local device DB for user management & system logs.
* Wifi Access point functionality for provisioning.
* Develop and Engineer the system.
* Provide documentation of the new system.
* Knowledge Transfer/Integrate with Mr Pandian.

LogicBots proposes to design, develop and provide installation of v1.0 of the proposed system to Mr Pandia. This activity will requires 5 weeks.

The Value Proposition of using LogicBots for this project are:
* Proven engineering techniques for making Integrated systems.
* Leveraging our experience in working with IoT toolkit (ESP) to bootstrap your effort. 
* Using subject matter experts to complete the project quickly. Rapid project completion minimizes disruptions and allows organizations to realize cost-saving quickly.

## Delivery Scope

* Project Definition
    - A review of the current system which helps in the firmware developing of the devices.
    - A project kickoff meeting to discuss and document the complete scope of this system and the goals and requirements of this project.

## Device APIs

Admin SDK / APIs to interact with the device 
* Using Serial Mode :-
  - To show the last swiped card id. 
  - For changing Serial number.

* Using Access Point Mode :-
  - Update Serial Number
  - Setting Time/Clock
  - Change device IP address
  - Update server URL
  - Add User with userId & card number
  - Delete user with userId
  - Add User with userId & live card detection for getting card number
  - Adding/Updating Wifi access point
  - Showing the Attendance logs

## Devices

* Data to Capture from Sensory Devices

```
RFID:           Reading the RFID cards

MEMORY CARD:    Acts as a local Database

RTC:            For real time calculation even after power shortage

```


## Maintenance (if required)
The period after the development for maintaining the product to be discussed with Mr. Pandian as it incurred extra charges.

## Exclusions
The followings are excluded from the project scope
* The packages used and maintained by LogicBots for interfacing with IoT Devices.

## Deliverables
The deliverables are listed below.

1. Wifi provisioning is provided on the end-user device so that end-user can easily connect their router to the system. Below is the step-wise guide. 
![WiFi Flow](https://github.com/ashtam55/Sow_brewing_automation/raw/master/Wifi%20provisioning%20flow.png)

2. Reader Mode - Running on ESP32 Core1 which detects the card, store in the DB, notifies the ESP32 Core 2 & turn the LSUCCESS LED for 0.5 sec. It also writes to the serial communication where a computer software read the detected tag and display on the screen.

3. Attendance Mode - On Core1 detects the card, verify the if the card number is valid, save in DB, notifies the Core 2 & turn the LSUCCESS LED for 0.5 sec, Core 1 will wait for notification from Core 2, as soon as  notification is received, loads current and unsent data and send to the http server url. 
Core 2 - if the designated url is not reachable, try every 30 seconds to check if the URL is reachable, as soon as reachable, send all unsent data one by one from oldest to latest.

4. Saving data to EEPROM - 	Serial number: 10 digit alpha numberic(which is unique for every device)
	                          Server url: 126 bytes
	                          Device ip : 4 bytes
                            
5. If serial number is empty, then system should act as act a wifi access point with default ip address ( if default gateway is 192.168.1.1, then default ip is 192.168.1.199, first 3 parts of ip should be same as the gateway ip)

6.	A button should be provided to make the device act as a wifi access point. 

7. When the device is in access point, user shall able to call a URL for perfoming following features:
	  - Update  serial number (this should be the very first operation, if serial number is writen, the same should not be edited. if serial number is not         updated, then no other operations should be allowed)
    - Update the current time
    - Update device IP address
    - Update the server url 
    - Add user with user id and card number
    - Add user with user id - after this call, LWAIT turns on, device will wait for card to swipe , and map the swipped card number to the user id, then         LWAIT truns off, LSUCCESS blinks, if the card is already mapped, LFAILED should blink.
    - Delete user with user id
    - View the attendance logs
    - Changing access point will not impact the behavior of Attendance Mode and Reader mode.
    - Time clock should run even after the restarting the device
    - SD card should be used for stroing user data and attendance logs
    - Attendance logs should be maximum of 10,000, beyond which, it will delete the oldest one and store the new one
    - User count is maximum 1000, beyound which, LFAILED should blink, and calling URL should return the failure code, 

8. Reading and editing the serial number should be allowed through serial communication through a computer software where we can edit and send the command to controller through serial communication. 

9. A computer software for providing the host level functionality which can able to read the serial data, copy & paste the data in cursor position, change the device serail number.

10. Software Access - top-level Git repositories for the hardware SDKs and APIs.

11. Documentation for the proposed changes in the system.

## Investment and Cost (To be discussed)
* Man-hour required: 5 weeks: 20 hours per week ( Sensor delivery time not included )

* Hardware required: On Cost  : 
    * RFID Sensor: [Link](https://robu.in/product/rdm6300-125khz-em4100-rfid-card-id-reader-module/)
    * RFID Card: [Link](https://robu.in/product/125khz-rfid-card/)
    * RTC: TBD by Mr. Pandian
    * Memory Card Sensor: TBD by Mr. Pandian
    * Memory Card: TBD by Mr. Pandian

 * Payment Schedule

| Milestone                                                      | Percentage    | Amount | 
| -------------                                                  |:-------------:| -----: |  
| Hardware ordering                                              | 0%            |Total Hardware cost as stated above |
| First working prototypes includes 1, 4, 5, 6                   | 40%           | $400 |
| Second working prototypes includes 2, 3, 7                     | 60%           | $600 |
| Third working prototypes includes 8, 9                         | 80%           | $400 |
| Software handover includes (10, 11) + Upwork Comission         | 100%          | $300 |

##### Upwork commission fee which is 20% upto $500 & 10% for more than $500 to be paid by the Mr. Pandian.
##### Devices/Sensors and delivery cost to be paid as a first milestone.
##### Milestone should be funded before LogicBots start working on that particular milestone on upwork.


## Customer Responsibilities
* The nature of this engagement dictates that LogicBots receive a frequent and enthusiastic response from the appropriate personnel.
* A weekly review between the LogicBots and Mr Pandian or his designate will ensure that the expectations of this engagement are met.
* Mr Pandian will assign a key contact who will be responsible for providing LogicBots with information, access to personnel, and facility access if required.
* Mr Pandian will provide a work area space with desk, chair, Internet access for use by LogicBots to conduct project business while working on-site.

## Acceptance Criteria
After this evaluation, all deliverables for this phase will be presented to Mr Pandian for review.

Mr Pandian or his representative will have Seven business days from the date of delivery of any document that is a deliverable to review it and request any changes. If LogicBots does not receive notification of any required changes within this period, the document will be deemed to have been accepted without modification and will be reissued as a final copy.

If LogicBots is notified by Mr Pandian, within the above time frame, of any changes required, LogicBots will within two business days of such notification implement those changes as have been agreed between the parties.  A final copy of the document will then be submitted to Mr Pandian.

## Assumptions
* General
    * All documentation created for this project will be available in hard copy and electronic format.
    * Any modifications to the scope of work will be handled through a change control process and will be agreed to by both parties.

* Commercial
    * Additional costs may be incurred where any delay not under the control of LogicBots that causes his personnel to not fulfil their scheduled tasks.
    * Mr Pandian will be available at the time of completion of the build phase so that all documentation can be accepted and signed.
    * Additional costs may be incurred where any work scheduled to be undertaken by LogicBots is postponed by Mr Pandian after 24 hours of its commencement.
    * All changes to the schedule or technical requirements must be provided to LogicBots in written format. Email is included as written format. Receipt of all correspondence should be confirmed by phone wherever possible.
    * Mr Pandian has accepted the costs/times estimate as detailed in this document
    * Mr Pandian has accepted the LogicBots standard terms and conditions mentioned above.


## Approved by
Name:   
Date:   
Position:   
