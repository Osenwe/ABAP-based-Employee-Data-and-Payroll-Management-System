# ABAP-based-Employee-Data-and-Payroll-Management-System
This is a project done for my a course in one of my graduate program (Masters Information Systems)
FINAL PROJECT REPORT BIS657

Employee Data and Payroll Management System
Prepared by: Andrew Benyeogor Osenwe                                  
Date Prepared: 11.30.2022
Status:  Final Report
Version:  1.0
Package ID: Z111
User: AUSER-111
Program: ZTERM_PROJECT_Z111	
TCODE: ZTP111
Login ID: 100001
Password: passinit

INTRODUCTION
Background Information
Benand's Bakeries, founded in 2018, is fast food joint that makes a variety of baked products for their customers, this business is based in Michigan with three business locations in Mount Pleasant, Alma, and Midland. In recent years, the bakery has experienced tremendous growth in terms of its customer base which has also led to an increase in the number of its employees from 20+ to 100+ employees. 
Benand’s Bakeries employees are paid on an hourly basis. Employees are also allowed to choose their work schedule timetable, but must keep to it else they drop in a leave request. For the business to manage its workforce, to allow for survival and further expansion an automated system will be needed to allow the admins to maintain employee's data, their timesheet records, create new or edit job positions, and generate payroll summaries for each pay period, and most importantly allow for some level of security to prevent unauthorized persons from gaining access.
Summary of the functionalities
Create, Save, edit, Update and User data,
Create, Save, edit, Update, Delete/Deactivate User Account Login details and view reports
Create, Save, edit, Update, View employee Leave requests (Approved, Declined, Pending)
Track all attempts to change user passwords (successful or unsuccessful)
Save, Edit, Update, view timesheet records
Generate summary payroll records from timesheet records for a particular date range, and a specific pay date.



OPEN ISSUES
This project was faced with some difficulties, the most important being time constraints. Adequate testing has not been performed to check out for potential bugs, but so far I have not encountered any errors.

Unable to connect the selection screen created in the ALV report with the module pool program.
Initial problem faced was determining what fields to use as primary keys in each table.
In screen 0300 table control, the position id column is blank, some non-fatal error in the code I am working on to correct. 
Due to time constraints I am not able to add functionality that helps prevent input error by users. For example, putting Time in as 7:30am and Time out as 4:00 am on the same day, in this case hours worked will be negative, thus user must ensure they put in the correct time. 
Knowledge needed to create this project came from my BIS657 class.
Additional sources of knowledge came from my experience with BIS638 class material’s, and some videos on Udemy, and YouTube.


FUNCTIONAL DESCRIPTION
To make the system more functional the following were created.
Seven (7) Normal screens and Five (5) Sub screens
Seven (7) custom database tables with custom made data elements
Three (4) ALV reports with selection screens to filter out the resulting reports based on certain criteria
Thirty-two (33) subroutines containing the logic which powers the functionalities.
 
Screens
Screen 0100: This screen is the main login page, only employees registered as Admins, and active will be able login as this project was created with admins in mind.

Screen 0200: This screen is the home page the admin sees after logging in. It allows the user to navigate to any task.












Screen 0300: This screen has been created to have several functionalities which includes
Saving Employee Data: Leave the Employee ID field blank, fill other details then click save. The employee ID, and other employees details such as state and country are auto generated on saving.

Updating Data: Put in employee id in the field, click edit, start editing the fields you need to change. Finally click Update.

Search: This allows the user to view the active and inactive employees in a particular business location, input Branch ID then click SEARCH




Screen 0400: This screen is the most complex in this project and has been created to offer the following functionalities.
Save new timesheets, Edit and Update existing timesheet records employees. This feature will be of great importance when the clock in the machine fails or an employee forgets to clock in.
Post summary payroll for all employees for a particular pay period, this information was gotten from the timesheet table using a number of SQL queries. Admins also have the opportunity to add the current tax rate and even a bonus sum when generating payroll. Below is a screenshot from the screen in action. I manually added a timesheet for two customers for 3 days, assuming they only came to work 3 days in the month of December 2022. I then generated a summary payroll with a tax rate of 2% and bonus pay of 100 USD. The result of the posting can also be seen in the report. The difference in payment is due to different hourly rates for the different job positions.

	




Screen 0500: Login details for a newly hired employee can be created through this screen, after his personal details might have been saved on screen 0300, else we get a warning message. Through this screen a current admin has the ability to make a non admin to become an admin. Deleting an employee record on this screen changes the status of that employee to inactive in all tables used in this project. 
To start editing a user login detail put in employee id, click edit, user details appear then change what details you need to then click update, admins are only allowed to change status and Account type.



Screen 0600: This screen allows users to manually enter, edit and save or update employee leave requests to take some days of work. 

New leave request: Fill in all fields except Leave ID. click save.

Editing Existing request: Fill in the leave period from and to, click ‘REFRESH’ search for the leave what to edit. For example, click the pending tab and choose a leave you might want to accept or reject. Copy the leave ID and paste in the “Leave ID field” click edit. The details of that leave appears on the screen. Click update when editing is complete.



Screen 0700: This screen allows users to change their passwords to a new one. However, the system won’t allow a new password that might have been used in the past by that employee and also the new password must not be the same as. Every attempt to change passwords both successful and unsuccessful leaves a trail that's recorded in the zpwdchange_111 table.



Reports
This project also featured four (4) ALV reports that showed the timesheet, payroll and user account details record. The reports names are:
ZALV_SCREEN_0400P: This displays the payroll summary data and select options based on the employee id and pay date.

ZALV_SCREEN_0400T: 	Displays timesheet records with select options based on the employee id and date range.

ZALV_SCREEN_0500: 	Display employee login account details.

ZALV_SCREEN_0500P:	Displays all password change attempts with select options based on employee id.
Custom Tables
The project requires some database tables to be fully functional, 7 custom database tables have been developed to this effect, this project allows admins to make some limited changes to the data contained within the table and they are briefly described below.
ZEMPLOYEEDATA111:  The purpose of this table is to store general data about employees and is the basis for the majority of the screens created in this project. 



















ZLOGINTABLE_111: 	This table's purpose is to store employees’ login details such as password, and it is the basis for the login screen, whenever an employee job has been terminated his detail must be deleted from this table so as to prevent them from logging back in, this functionality can be found on screen ‘0500’, the nature of the primary key here allows an employee to have more than one login details as long as it is created on different days.
. 


ZPWDCHANGE_111:	The purpose of this table tracks all attempts to make password changes to any account.  As a security measure it stores information about the date and timestamps when password changes were made, and most importantly stores a history of the previous passwords used by an employee. Admins won't be able to make changes to the data in this table but can only view the reports. The STAT column in the table is an auto generated comment on the password change.



ZEMPLOYEELEAV111:	The purpose of this table is to store information about all leave requests such as study, sick leave etc., an employee might issue.








ZJOBS_111:	This table stores information about various job positions such as titles and hourly rate for that particular job position, using SQL queries in conjunction with the ZEMPLOYEEDATA111 we get information that makes the timesheet table more complete. 



ZTIMESHEET_111:	This table stores basic information about the history of every employee's completed work shifts. This table will be of great importance in creating the payroll table.



ZPAYROLL_111: This table stores information about all salary payments that have been received by the employees.  Data in this table will be auto generated from the ZTIMESHEET_111 table on every pay date period.







  
PROCESS FLOW

Navigation
In designing this project, care was taken to ensure a smooth navigation between the various screens and reports. The diagram below gives an overview.  rpt 1,2,3, and 4 signifies the ALV reports. The navigation style shown below gives the user some flexibility in choosing a task to do.



SIMILAR FUNCTIONALITIES NOT IN PROJECT
 The following similar functionalities were not added to this project because they are out of scope
Ability to create new and edit job positions.
Ability to create new, save, edit branch locations, automatically generate the number of workers in that branch.
Use of interactive ALV reports.