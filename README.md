# ABAP-based-Employee-Data-and-Payroll-Management-System
This is a project done for my a course in one of my graduate program (Masters Information Systems)

INTRODUCTION
 This purpose of this project is to simulate some employees data maintenance functinalities. I observed while working at CMU dining, but with SAP ABAP.
Summary of the functionalities
Create, Save, edit, Update and User data,
Create, Save, edit, Update, Delete/Deactivate User Account Login details and view reports
Create, Save, edit, Update, View employee Leave requests (Approved, Declined, Pending)
Track all attempts to change user passwords (successful or unsuccessful)
Save, Edit, Update, view timesheet records
Generate summary payroll records from timesheet records for a particular date range, and a specific pay date.


FUNCTIONAL DESCRIPTION
To make the system more functional the following were created.
Seven (7) Normal screens and Five (5) Sub screens
Seven (7) custom database tables with custom made data elements
Three (4) ALV reports with selection screens to filter out the resulting reports based on certain criteria
Thirty-two (33) subroutines containing the logic which powers the functionalities.
 
Screens
Screen 0100: This screen is the main login page, only employees registered as Admins, and active will be able login as this project was created with admins in mind.

![0100](https://user-images.githubusercontent.com/68793142/205477361-274b8222-067c-476a-84ab-df16427078bb.png)

Screen 0200: This screen is the home page the admin sees after logging in. It allows the user to navigate to any task.

![0200](https://user-images.githubusercontent.com/68793142/205477403-59d521fc-d022-4cc9-80fa-a6da9f5a5692.png)


Screen 0300: This screen has been created to have several functionalities which includes
Saving Employee Data: Leave the Employee ID field blank, fill other details then click save. The employee ID, and other employees details such as state and country are auto generated on saving.


Updating Data: Put in employee id in the field, click edit, start editing the fields you need to change. Finally click Update.



Search: This allows the user to view the active and inactive employees in a particular business location, input Branch ID then click SEARCH

![0300](https://user-images.githubusercontent.com/68793142/205477405-200143d9-2da5-4a08-83db-887eaaafd40c.png)



Screen 0400: This screen is the most complex in this project and has been created to offer the following functionalities.
Save new timesheets, Edit and Update existing timesheet records employees. This feature will be of great importance when the clock in the machine fails or an employee forgets to clock in.
Post summary payroll for all employees for a particular pay period, this information was gotten from the timesheet table using a number of SQL queries. Admins also have the opportunity to add the current tax rate and even a bonus sum when generating payroll. Below is a screenshot from the screen in action. I manually added a timesheet for two customers for 3 days, assuming they only came to work 3 days in the month of December 2022. I then generated a summary payroll with a tax rate of 2% and bonus pay of 100 USD. The result of the posting can also be seen in the report. The difference in payment is due to different hourly rates for the different job positions.

![0400](https://user-images.githubusercontent.com/68793142/205477406-38ff4258-0710-4be1-bb7c-b0d8299ad49e.png)	

![payroll report](https://user-images.githubusercontent.com/68793142/205477492-4a071c88-bedb-4b27-bfc6-899f90095c2c.png)


Screen 0500: Login details for a newly hired employee can be created through this screen, after his personal details might have been saved on screen 0300, else we get a warning message. Through this screen a current admin has the ability to make a non admin to become an admin. Deleting an employee record on this screen changes the status of that employee to inactive in all tables used in this project. 
To start editing a user login detail put in employee id, click edit, user details appear then change what details you need to then click update, admins are only allowed to change status and Account type.

![0500](https://user-images.githubusercontent.com/68793142/205477407-9685acf6-2607-4781-bf64-aba704e7d555.png)


Screen 0600: This screen allows users to manually enter, edit and save or update employee leave requests to take some days of work. 

New leave request: Fill in all fields except Leave ID. click save.

Editing Existing request: Fill in the leave period from and to, click ‘REFRESH’ search for the leave what to edit. For example, click the pending tab and choose a leave you might want to accept or reject. Copy the leave ID and paste in the “Leave ID field” click edit. The details of that leave appears on the screen. Click update when editing is complete.

![0600](https://user-images.githubusercontent.com/68793142/205477526-3601a5c7-2aa4-40e2-a6cf-5390e278a57f.png)

Screen 0700: This screen allows users to change their passwords to a new one. However, the system won’t allow a new password that might have been used in the past by that employee and also the new password must not be the same as. Every attempt to change passwords both successful and unsuccessful leaves a trail that's recorded in the zpwdchange_111 table.

![0700](https://user-images.githubusercontent.com/68793142/205477402-927bce80-0ca4-4fdf-b750-f8a5e20e5ef5.png)

Reports
This project also featured four (4) ALV reports that showed the timesheet, payroll and user account details record. The reports names are:
ZALV_SCREEN_0400P: This displays the payroll summary data and select options based on the employee id and pay date.

ZALV_SCREEN_0400T: 	Displays timesheet records with select options based on the employee id and date range.

ZALV_SCREEN_0500: 	Display employee login account details.

ZALV_SCREEN_0500P:	Displays all password change attempts with select options based on employee id.

Custom Tables
The project requires some database tables to be fully functional, 7 custom database tables have been developed to this effect, this project allows admins to make some limited changes to the data contained within the table and they are briefly described below.

ZEMPLOYEEDATA111:  The purpose of this table is to store general data about employees and is the basis for the majority of the screens created in this project. 

![zemployeeleav111](https://user-images.githubusercontent.com/68793142/205477502-ac39d46c-5fc7-4fa3-b019-a1f8f8727730.png)

ZLOGINTABLE_111: 	This table's purpose is to store employees’ login details such as password, and it is the basis for the login screen, whenever an employee job has been terminated his detail must be deleted from this table so as to prevent them from logging back in, this functionality can be found on screen ‘0500’, the nature of the primary key here allows an employee to have more than one login details as long as it is created on different days.
 
![zlogintable_111](https://user-images.githubusercontent.com/68793142/205477504-0705a049-9a99-4402-af26-b4fa056ced36.png)

ZPWDCHANGE_111:	The purpose of this table tracks all attempts to make password changes to any account.  As a security measure it stores information about the date and timestamps when password changes were made, and most importantly stores a history of the previous passwords used by an employee. Admins won't be able to make changes to the data in this table but can only view the reports. The STAT column in the table is an auto generated comment on the password change.

![zpwdchange_111](https://user-images.githubusercontent.com/68793142/205477506-84a3defc-edbc-4014-837b-cdbe9d6a0bc3.png)


ZEMPLOYEELEAV111:	The purpose of this table is to store information about all leave requests such as study, sick leave etc., an employee might issue.
![zemployeedata111](https://user-images.githubusercontent.com/68793142/205477501-cd2cd65f-b999-482d-bbaf-fc86884e4792.png)








ZJOBS_111:	This table stores information about various job positions such as titles and hourly rate for that particular job position, using SQL queries in conjunction with the ZEMPLOYEEDATA111 we get information that makes the timesheet table more complete. 
![zjobs_111](https://user-images.githubusercontent.com/68793142/205477503-fbb5e650-4f65-4766-a1f1-54aedb2b2f29.png)



ZTIMESHEET_111:	This table stores basic information about the history of every employee's completed work shifts. This table will be of great importance in creating the payroll table.
![ztimesheet111](https://user-images.githubusercontent.com/68793142/205477500-692af014-de64-43af-a4f0-901c7ec28243.png)


ZPAYROLL_111: This table stores information about all salary payments that have been received by the employees.  Data in this table will be auto generated from the ZTIMESHEET_111 table on every pay date period.

![zpayroll_111](https://user-images.githubusercontent.com/68793142/205477505-a37b185a-8970-4192-a095-883ec125e092.png)





  
PROCESS FLOW

Navigation
In designing this project, care was taken to ensure a smooth navigation between the various screens and reports. The diagram below gives an overview.  rpt 1,2,3, and 4 signifies the ALV reports. The navigation style shown below gives the user some flexibility in choosing a task to do.
![navigation](https://user-images.githubusercontent.com/68793142/205477645-8973fbe3-b9f0-4f14-b2f4-26e11a1a6663.png)



SIMILAR FUNCTIONALITIES NOT IN PROJECT
 The following similar functionalities were not added to this project because they are out of scope
Ability to create new and edit job positions.
Ability to create new, save, edit branch locations, automatically generate the number of workers in that branch.
Use of interactive ALV reports.
