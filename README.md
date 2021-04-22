# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. A valid csv file must be present 
3. A data converter to PDF format is required as the output is to be reported in PDF format
4. Notification utiilities must be present
5. Read/Write access to the location where the PDF reports have to be stored

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | We require a valid PDF converter to convert the data from csv format to PDF reports
Counting the breaches       | Yes           | As this is part of the requirement, we need to implement the tests to check the total breaches over the month
Detecting trends            | Yes           | We need this to detect the trend when the reading was continuously increasing for 30 minutes
Notification utility        | Yes           | We need to check whether the notifications are being sent properly or not

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "Null Utility" when the notification utility is not available
4. Write the count of breaches to the PDF crossed over the month
5. Write the recorded trends to the PDF when the reading was continuously increasing for 30 minutes
6. Write mock tests to check the notification utilities
7. Write "No storgage container" when there is no access to the storage locator
8. Tests to check access to the server on which the csv file is present
9. Write "No input file found" when there is no valid csv file on the server.
10. Write "New report available" when there is a new PDF report generated.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | new report available        | Mock report generate
Report inaccessible server | Server addess | Unable to acess the report | Fake file dependency
Find minimum and maximum   | CSV File     | Maximum & minimum readings  | None - it's a pure function
Detect trend               | CSV file     | Detect trends with timestamp| None - it's a pure function
Write to PDF               | CSV file     | PDF report generated        | Mock PDF report generation
