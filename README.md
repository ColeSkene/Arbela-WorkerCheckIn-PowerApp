# Arbela-WorkerCheckIn-PowerApp
This is an employee/student check-in app which starts the process by taking their picture and verifying that they don’t have any COVID symptoms (by asking simple Yes/No questions) before letting them into the building.
# Installation Instructions
## Prerequisites
	• Have access to an Office 365 User with a Power Apps license
	• Have system admin access to a target power apps environment where the solution will be deployed
	• Download the Managed Solution file "WorkerCheckinTools_1_0_0_3_managed"
	• Download all Sample Data files (.xlsx)

## Install Solution
	1. Go to https://make.powerapps.com/, select your target environment, and open "Solutions"
		○ If you do not have a Power Apps license, sign up for the Power Apps Community Plan
		○ If you do not have an environment, create one through the Power Platform Admin Center
	2. From the Solutions screen, select "Import" in the Command Bar
	3. Within the Import Solution dialog, select "Choose File" and select the "WorkerCheckinTools_1_0_0_3_managed" file downloaded previously
	4. Proceed through the dialog window with defaults selected and initiate the solution import process
	5. When complete, there may be warnings noted, but this is ok as long as the Solution has been installed

## Activate Flows
	1. From the Solutions screen, open the Worker Check-In Tools solution
	2. At the right side of the Command Bar, select Flow in the drop-down menu to filter the list
	3. Open the "Internal Notifications - Questionnaire Failure Alert" flow and click "Edit" in the Command Bar
		a. Add CDS and Office 365 Outlook connections to the Flow
			§ Note: the Office 365 Outlook connection will define the sender address of the Email
		b. In the "Send Email Alert" step (Office 365 Outlook) specify an appropriate User, Email Address, or Distribution List in the "To" field
			§ This is the address to which automated failure notification emails will be sent
		c. When complete, Save the Flow and return to the Flow details screen
		d. Click "Turn on" in the Command Bar to activate the Flow and close the tab when activation has been confirmed
	4. From the Worker Check-In Tools solution in the Power Apps Maker Portal, open the "Worker Check in Responses - Associate worker check in submission" flow and click "Edit" in the Command Bar
		a. Update CDS Steps with the previously created CDS Connection
		b. When complete, Save the Flow and return to the Flow details screen
		c. Click "Turn on" in the Command Bar to activate the Flow and close the tab when activation has been confirmed

## Edit Site Map
	1. Open the Worker Check-In Tools solution
	2. At the right side of the Command Bar, select Canvas App in the drop-down menu to filter the list
	3. Select the "Worker Check In App" to open its details screen
		a. From the details screen, copy the "Web Link" to your clipboard (right click > copy link address)
		b. Select "Worker Check-In Tools" below the Command Bar to return back to the Worker Check-In Tools Solution
	4. At the right side of the Command Bar, select Other in the drop-down menu to filter the list
	5. Select the "Worker Check In Management App" Site Map component to open the Sitemap Designer
		a. From the Sitemap Designer, select the "Check-in App" subarea under the "Links" group to reveal its properties on the right
		b. From the Subarea properties pane, paste the previously copied URL into the corresponding text field
		c. At the top right of the Sitemap Designer, click Save, then Publish, then Save And Close
	
## Import Sample Data (Part 1)
	1. Open the Worker Check-In Tools solution
	2. At the right side of the Command Bar, select Model-driven App in the drop-down menu to filter the list
	3. Select the "Worker Check-In Management App" component to open the App Designer, and click "Play" to run the Model-driven App
	4. From the Worker Check-In Management App, click "Language Profiles" under the Configuration section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Language Profiles (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find two sample Language Profiles present in the "Active Worker Check In Language Profiles" view

## Configure Data-dependent Processes
	1. From the Solutions screen, click the "New Solution" button at the left side of the Command Bar
	2. In the New Solution pane which pulls out from the right, enter the following values:
		a. Display Name: Worker Check-In Tools Customizations
		b. Name: [auto-populated]
		c. Publisher: [your preferred publisher]
		d. Version: [Leave as default]
	3. Click "Create" to create and open the new solution
	4. From the Worker Check-In Tools Customizations solution, click "Add Existing" in the Command Bar and select "Process" from the drop-down list and do the following:
		a. Find and select the Process named "Worker Check-in App - Create Localized Label for Default Language"
		b. Click "add" at the bottom left of the pull-out pane
	5. Open the "Worker Check-in App - Create Localized Label for Default Language" Workflow
		a. From the Process Information form, Click "Deactivate" in the ribbon to edit the process
		b. At the bottom of the form, click "Set Properties" for the single step labeled "Create English Localized Label"
		c. In the Step Properties window, clear any value present for "Language" and set to the "English" record previously imported
		d. Click "Save and Close" to exit the Step Properties window
		e. Click "Activate" to reactivate the Workflow
		f. Close the window to return to the Maker Portal

## Import Sample Data (Part 2)
	1. Click "Questions" under the Configuration section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Questions (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find seven sample Questions present in the "Active Worker Check In Questions" view
	2. Click "Localized Labels" under the Reference section of the site map on the left side of the screen
		a. Note the seven English Localized Labels corresponding to the Questions previously imported
		b. Click "Import from Excel"
		c. Click "Choose File" then navigate to and select the "Localized Labels (Sample).xlsx" downloaded previously
		d. Proceed through the wizard and select "Finish Import" to initiate the import
		e. After a few seconds, refresh to find seven new Spanish sample Language Profiles present in the "Active Worker Check In Question Localized Labels" view
	3. Click "Locations" under the Configuration section of the site map on the left side of the screen
		a. Click "New"
		b. Enter a Location name ("Default Location" may suffice for now)
		c. Select "English" as the Default Language
		d. Select a Timezone
		e. Click "Save" to create the record
		f. On the form, click the "Related" tab, to the right of "General" and select "Worker Check-In Questions" from the drop-down list
		g. From the Associated View, click "Add Existing Worker C…" (Add Existing Worker Check-In Question)
		h. From the pull-out menu on the right, click "Enter" on your Keyboard to browse all records
		i. Select all records one by one, and once the list is empty, click "Add" at the bottom of the pull-out menu
		j. Click "Save & Close"
	4. Click "Settings Profiles" under the Configuration section of the site map on the left side of the screen
		a. Click "New"
		b. Enter a Settings Profile name ("Default Profile" or "My Profile" may suffice for now)
		c. Select "Default Location" as the Default Location
		d. Enter "0" as your default camera number
		e. Click "Save & Close" to create the record


## Test the Check-in App Configuration Settings
	• From the Worker Check-In Management App, click "Check-in App" under the Links section of the site map on the left side of the screen
	• If prompted, click "Allow" to grant Camera permissions  or any others requested by the App
	• From the Worker Check-In App:
		○ Select "App Config" and note that the Settings Profile and Location records created earlier are present in the Form
			§ Click the Home Icon at the top left of the screen to return to the Home Screen
		○ Select "Camera Config" and note that the previously entered "default Camera Number" is present in the field on the left side
			§ Use this screen to select the correct (typically forward facing) camera to use in the app, starting with zero, in increments of 1 until the correct camera is found
			§ Once found, click "Set Default" to update your Settings Profile with this correct Default Camera Number
				□ After doing so, you can check the Model-driven App to confirm this change went through
			§ Click the Home Icon at the top left of the screen to return to the Home Screen
		○ Select "Session Details" note the values for User Settings, Location, and Language Profile to confirm they are set as expected
			§ Click the Home Icon at the top left of the screen to return to the Home Screen
		○ Select "Questionnaire" to reveal the Welcome Screen for the Worker Check-In Experience

## Test the Check-in App Questionnaire
	• Welcome Screen
		○ Note that the Welcome Screen contains the following elements w/ text corresponding to the selected default Language Profile:
			§ Header Text
			§ Welcome Label
			§ Toggle Entry Mode Button
			§ Field Name
			§ Submit Button
			§ Cancel Button
		○ Enter "Test" as an Employee Id and click "Submit"
		○ Note that while not in Manual Entry Mode the system awaits Keyboard input (from an RFID scanner or otherwise) and will continue automatically when input is detected
	• Language Screen
		○ Note that the Select Language screen shows each Language Profile imported previously and identifies each by the record's "Display Name" attribute
		○ Select "English" to continue
	• Information Screen
		○ Note that an "Information Screen" is displayed the first time "Test" is used as the Employee Id to answer the Questionnaire
			§ This will be skipped in subsequent runs with the same Employee Id
		○ Click/Tap anywhere to continue
	• Selfie Screen
		○ Note that the Camera screen will automatically capture an image after a 5 second countdown and options will be presented to "Continue" or "Retake"
	• Questionnaire Screen
		○ Note that the Questionnaire Screen contains the following elements w/ text corresponding to the selected default Language Profile:
			§ Header Text
			§ Yes Button
			§ No Button
		○ Note that the Questions displayed are associated with the Default Location as specified in the current Settings Profile record
		○ Note that, for each Question Displayed, the text shown is that of the associated Localized Label related to the Language Profile selected previously
		○ Note that after the first question is answered, a back button will appear in the upper left corner of the screen for all subsequent questions, allowing users to go back and change their answer for previous questions
		○ Note that after 20 seconds of inactivity, the Questionnaire will begin to "Timeout" with a 10 second countdown timer with Yes/No options to Quit/Abandon the questionnaire
	• Disposition Screen
		○ Note that after answering all questions with values corresponding to the Question's "Expected Response" attribute, this screen will display the Language Profile's "Label: Disposition Message (Pass)" value with a corresponding smiley face icon
			§ Otherwise, the Language Profile's "Label: Disposition Message (Fail)" value will be displayed with an "X" Icon
		○ Note that the App will navigate back to the Questionnaire Welcome Screen after clicking/tapping anywhere on the Disposition Screen, or after a silent 10 second countdown
			§ Note that a subsequent

## Validate Questionnaire Data
	• From the Worker Check-In Management App:
		○ Click "Submissions" under the Core section of the site map on the left side of the screen
			§ Note that Submissions have been created for any Questionnaire sessions initiated by entering an Employee Id
			§ Open a completed Submission record (one containing an End Time) to view information including:
				□ Employee Id
				□ Start & End Times
				□ Image captured
			§ From an open Submission record, click the "Related" tab, to the right of "General" and select "Worker Check-In Responses" from the drop-down list
				□ Note the associated Responses for each question presented in the Questionnaire for this Worker are contained within this Associated View, indicating which question was asked, and what the Worker's response was
		○ Click "Login History" under the Reference section of the site map on the left side of the screen
			§ Note that Login History records exist for Employee Id "Test" and any other values for which a Questionnaire was completed
	
