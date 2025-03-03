# Program rules supported in Android Capture App { #capture_app_pr }

The following is a comprehensive list of all Program Rule components (variable types and actions) available in DHIS2, and notes on whether or not these have been implemented in the DHIS2 Android App.

> **Note**
> 
> Any issues around using a particular feature with Android are highlighted with an exclamation mark !.

|legend|description|
|:--:|:------|
|![](/en/resources/images/admin/icon-complete.png)|Value type implemented|
|![](/en/resources/images/admin/icon-incomplete.png)|Value type not implemented, but will be safely ignored (if not compulsory) |
|![](/en/resources/images/admin/icon-na.png)|Not applicable|
|![](/en/resources/images/admin/icon-wip.png)|Work in progress. Feature not completely implemented yet or with unexpected behavior already reported |

## Program rule Variable source types supported { #capture_app_pr_prv }

| Variable type| Description of variable type| Program with registration| Program without registration| Notes on implementation|
|-|-----|:-:|:-:|-----|
|Data Element from the newest event for a program stage|This source type works the same way as "Data element from the newest event in the current program", except that it only evaluates values from a specific program stage.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Data element from the newest event in the current program (with registration)|This source type is populated with the newest data value collected for the specified data element within the enrolment.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Data Element from the newest event in the current program (without registration)|This program rule variable will be populated with the newest data value found within the 10 newest events in the same organization unit.|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-complete.png)||
|Data Element in current event (with registration)|Variable takes the data element&rsquo;s value from the current event.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Data Element in current event (without registration)|Contains the data value from the same event that the user currently has open.|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-complete.png)||
|Data Element from previous event (with registration)|Program rule variables with this source type will contain the newest value from all previous events for the specified data element. The event currently open is not evaluated.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Data Element from previous event (without registration)|This program rule variable will be populated with the newest data value found within the 10 events preceding the current event date (i.e. not including the current event).|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-complete.png)||
|Tracked Entity Attribute|Populates the program rule variable with a specified tracked entity attribute for the current TEI (e.g. current patient).|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Calculated value|Calculated value.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||

## Program rule Actions supported (Data element in current event) { #capture_app_pr_pra }

| Action| Description of action| Program with registration| Program without registration| Notes on implementation|
|-|-----|:-:|:-:|-----|
|Hide Field|Hides an individual data element if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|! If you change the value after the field is hidden, it will revert the action depending on the value type rule engine default value. We recommend its use combined with the hasvalue function.|
|Hide Section|Hides a whole section and its data elements if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Hide Option|Hide a single option for an option set in a given data element/tracked entity attribute. When combined with <b>show option group</b> the <b>hide option</b> takes precedence|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Hide Option Group|Hide all options in a given option group and data element/tracked entity attribute. When combined with <b>show option group</b> the <b>hide option</b> takes precedence |![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Show option group|Used to show only options from a given option group in a given data element/tracked entity attribute. To show an option group implicitly hides all options that is not part of the group(s) that is shown.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Assign Value|Assigns a value to a specified data element or attribute if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|To assing text, it must be in single quotes. For example: '2+2' will show the text 2+2 and 2+2, without the single quotes will show 4. |
|Show Warning|Shows pop-up warning to the user if rule is true; does not prevent the user from continuing.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Warning on Complete|Shows a pop-up warning to the user if, at the point &lsquo;complete&rsquo; is clicked, a rule is true; this does not prevent the user from continuing.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Show Error|Shows a pop-up error message to the user as soon as a rule is true, and prevents user from continuing until rule is no longer true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|The value is not saved, but the text is not cleared so that the user can fix it easily.|
|Error on Complete|Shows a pop-up warning to the user if, when "complete"; is clicked, a rule is true, and prevents user from continuing until rule is no longer true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Make Field Mandatory|Sets a data element as "mandatory"; if rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Display Text (Event Programs)|Used to display information that is not an error or a warning, for example feedback.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)| Independently from the source variable type, text will be displayed in the form as the last element of the last section. Text will be displayed as the messages in the indicators tab.|
|Display Text (Tracker Programs)|Used to display information that is not an error or a warning, for example feedback.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>1. Program rule configured as "Trigger rule only for program stage".</b> Text will be displayed ONLY in the form as the last element of the last section. Text will be displayed as the messages in the indicators tab. </br>-> If the program rule uses any variable type which is not from the current stage, the rule will not be able to evaluate and the message will not be shown.</br><b>2. Program rule NOT configured as "Trigger rule only for program stage".</b> Text will be displayed ONLY in the indicators tab and NOT in the form.</br>--> If the program rule uses any variable of type Current event, the rule will not be able to evaluate and the message will not be shown.|
|Display Key Value/Pair (Event Programs)|Used to display information drawn from a data element.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>Variable Type:</b> </br>* Data element from the newest event in the current program</br>* Data element from previous event</br>* Data element in current event</br>* Built-in variable</br>Key/Value Pair will be displayed in the form ONLY in the specified section.|
|Display Key Value/Pair (Traker Programs)|Used to display information drawn from a data element.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>1. Variable Type:</b></br>* Data element in current event</br>Key/Value Pair will be displayed in the form ONLY in the specified section.</br><b>2. Variable Type:</b></br>* Data element from the newest event in the current program</br>* Data element from previous event</br>* Data element from the newest event for a program stage</br>* Tracked entity attribute</br>* Built-in variable</br>Key/Value Pair will be displayed ONLY in the indicators tab and NOT in the form.|
|Hide Program Stage|Hides a whole program stage from the user if the rule is true.|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|Action rule only supported for <b>Data element from the newest event in the current program type and tracked entity </b> attribute variables.|
|Send Message|Send Message triggers a notification based on provided message template.This action will be taken whenever there is a change in data value. However this behaviour can be controlled by providing event-enrollment status in program rule expression|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|This feature is executed on the server side.|
|Schedule Message|Schedule Message will schedule notification at date provided by Expression in the data field.|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|This feature is executed on the server side.|

## Program rule Actions supported (Other variables) { #capture_app_pr_pra_other }

| Action| Description of Action| Data Element from the Newest Event in the Current Program (with registration)|Data Element from the Newest Event in the Current Program (without registration)| Data Element from Previous Event (with registration) |Data Element from Previous Event (without registration)| Data Element from the Newest Event for a Program Stage (with registration)|Tracked Entity Atribute (with registration) |Notes on implementation|
|-|-----|:-:|:-:|:-:|:-:|:-:|:-:|-----|
|Hide Field|Hides an individual data element if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Hide Section|Hides a whole section and its data elements if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Hide Option|Hide a single option for an option set in a given data element/tracked entity attribute. When combined with <b>show option group</b> the <b>hide option</b> takes precedence.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Hide Option Group|Hide all options in a given option group and data element/tracked entity attribute.When combined with show option group the hide option takes precedence.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Assign Value|Assigns a value to a specified data element or attribute if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|To assing text, it must be in single quotes. For example: '2+2' will show the text 2+2 and 2+2, without the single quotes will show 4.|
|Show Warning|Shows pop-up warning to the user if rule is true; does not prevent the user from continuing.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Warning on Complete|Shows a pop-up warning to the user if, at the point "complete" is clicked, a rule is true; this does not prevent the user from continuing.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Show Error|Shows a pop-up error message to the user as soon as a rule is true, and prevents user from continuing until rule is no longer true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|The rule will let the user to finish the enrollment but will prevent from completing the events until rule is no longer true. The value is not saved, but the text is not cleared so that the user can fix it easily.|
|Error on Complete|Shows a pop-up warning to the user if, at the point "complete" is clicked, a rule is true; this does not prevent the user from continuing.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)||
|Make Field Mandatory|Sets a data element as "mandatory" if rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)||
|Display Text (Event Programs)|Used to display information that is not an error or a warning, for example feedback.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)| Independently from the source variable type, text will be displayed in the form as the last element of the last section. Text will be displayed as the messages in the indicators tab.|
|Display Text (Tracker Programs)|Used to display information that is not an error or a warning, for example feedback.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>1. Program rule configured as "Trigger rule only for program stage".</b> Text will be displayed ONLY in the form as the last element of the last section. Text will be displayed as the messages in the indicators tab. </br>-> If the program rule uses any variable type which is not from the current stage, the rule will not be able to evaluate and the message will not be shown.</br><b>2. Program rule NOT configured as "Trigger rule only for program stage".</b> Text will be displayed ONLY in the indicators tab and NOT in the form.</br>--> If the program rule uses any variable of type Current event, the rule will not be able to evaluate and the message will not be shown.|
|Display Key Value/Pair (Event Programs)|Used to display information drawn from a data element.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>Variable Type:</b> </br>* Data element from the newest event in the current program</br>* Data element from previous event</br>* Data element in current event</br>* Built-in variable</br>Key/Value Pair will be displayed in the form ONLY in the specified section.|
|Display Key Value/Pair (Traker Programs)|Used to display information drawn from a data element.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-complete.png)|<b>1. Variable Type:</b></br>* Data element in current event</br>Key/Value Pair will be displayed in the form ONLY in the specified section.</br><b>2. Variable Type:</b></br>* Data element from the newest event in the current program</br>* Data element from previous event</br>* Data element from the newest event for a program stage</br>* Tracked entity attribute</br>* Built-in variable</br>Key/Value Pair will be displayed ONLY in the indicators tab and NOT in the form.|
|Hide Program Stage|Hides a whole program stage from the user if the rule is true.|![](/en/resources/images/admin/icon-complete.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-complete.png)|Action rule only supported for <b>Data element from the newest event in the current program variable </b> type. If the event is auto-generated, the rule will not apply.|
|Send Message|Send Message triggers a notification based on provided message template.This action will be taken whenever there is a change in data value. However this behaviour can be controlled by providing event-enrollment status in program rule expression|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|This feature is executed on the server side.|
|Schedule Message|Schedule Message will schedule notification at date provided by Expression in the data field.|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|![](/en/resources/images/admin/icon-na.png)|This feature is executed on the server side.|

## Functions to use in program rule expressions { #capture_app_pr_pre }

| Function   | Description of function | Status        | Notes on implementation |
| ---- | ----------------------------- | :----: | -- |
| d2:ceil    | Rounds the input argument up to the nearest whole number.   | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:floor   | Rounds the input argument down to the nearest whole number. | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:round   | Rounds the input argument to the nearest whole number.      | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:modulus | Produces the modulus when dividing the first with the second argument.        | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:zing    | Evaluates the argument of type number to zero if the value is negative, otherwise to the value itself.   | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:oizp    | Evaluates the argument of type number to one if the value is zero or positive, otherwise to zero.        | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:concatenate      | Produces a string concatenated string from the input parameters. Supports any number of parameters.      | ![](/en/resources/images/admin/icon-complete.png)    |Use d2:concatenate function instead of using "+" as the expression evaluator in the app will be adding numbers if it can.|
| d2:daysBetween      | Produces the number of days between the first and second argument. If the second argument date is before the first argument,  the return value will be the negative number of days between the two dates. The static date format is 'yyyy-MM-dd'.        | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:weeksBetween     | Produces the number of full weeks between the first and second argument. If the second argument date is before the first argument,  the return value will be the negative number of weeks between the two dates. The static date format is 'yyyy-MM-dd'. | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:monthsBetween    | Produces the number of full months between the first and second argument. If the second argument date is before the first argument the return value will be the negative number of months between the two dates. The static date format is 'yyyy-MM-dd'. | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:yearsBetween     | Produces the number of years between the first and second argument. If the second argument date is before the first argument, the return value will be the negative number of years between the two dates. The static date format is 'yyyy-MM-dd'.       | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:addDays | Produces a date based on the first argument date, adding the second argument number of days.    | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:count   | Counts the number of values that is entered for the source field in the argument.      | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:countIfValue     | Counts the number of matching values that is entered for the source field in the first argument. Only occurrences that matches the second argument is counted. | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:countIfZeroPos   | Counts the number of values that is zero or positive entered for the source field in the argument. The source field parameter is the name of one of the defined source fields in the program.      | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:hasValue         | Returns the number of numeric zero and positive values among the given object arguments. Can be provided with any number of arguments.       | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:validatePattern  | Evaluates to true if the input text is an exact match with the supplied regular expression pattern. The regular expression needs to be escaped.       | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:left    | Evaluates to the left part of a text, num-chars from the first character.     | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:right   | Evaluates to the right part of a text, num-chars from the last character.     | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:substring        | Evaluates to the part of a string specified by the start and end character number.     | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:split   | Split the text by delimiter, and keep the nth element (0 is the first).       | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:length  | Find the length of a string.     | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:zpvc    | Returns the number of numeric zero and positive values among the given object arguments. Can be provided any number of arguments.   | ![](/en/resources/images/admin/icon-complete.png)    | |
| d2:inOrgUnitGroup\* | Evaluates whether the current organization unit is in the argument group. The argument can be defined with either ID or organization unit group code. | ![](/en/resources/images/admin/icon-complete.png) | |
| d2:hasUserRole\** |Returns true if the current user has this role otherwise false.| ![](/en/resources/images/admin/icon-complete.png) | |
| d2:zScoreWFA\*** |Function calculates z-score based on data provided by WHO weight-for-age indicator. Its value varies between -3.5 to 3.5 depending upon the value of weight.| ![](/en/resources/images/admin/icon-complete.png) | |

> **Note**
>
> * Available in DHIS2 v2.30
> ** Available in DHIS2 v2.31 and greater
> *** Available in DHIS2 v2.32 and greater

## Standard variables to use in program rule expressions { #capture_app_pr_standard_vars }

Available in DHIS2 v2.30

| Variable     | Description of function       | Status | Notes on implementation |
| --- | -------------------------------------------- | :---: | -- |
| V{current_date}       | Contains the current date whenever the rule is executed. | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{event_date}         | Contains the event date of the current event execution. Will not have a value at the moment the rule is executed as part of the registration form. | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{event_status}         | Contains status of the current event or enrollment. | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{due_date} \*        | This variable will contain the current date when the rule is executed. Note: This means that the rule might produce different results at different times, even if nothing else has changed.     | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{event_count}        | Contains the total number of events in the enrollment.   | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{enrollment_date} \* | Contains the enrollment date of the current enrollment. Will not have a value for single event programs.       | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{incident_date} \*   | Contains the incident date of the current enrollment. Will not have a value for single event programs.         | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{enrollment_id} \*   | Universal identifier string(UID) of the current enrollment. Will not have a value for single event programs.   | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{event_id}  | Universal identifier string(UID) of the current event context. Will not have a value at the moment the rule is executed as part of the registration form.   | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{orgunit_code}       | Contains the code of the orgunit that is linked to the current enrollment. For single event programs the code from the current event Org Unit will be used instead.  | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{environment}        | Contains a code representing the current runtime environment for the rules. The possible values is "WebClient", "AndroidClient" and "Server". Can be used when a program rule is only supposed to run in one or more of the client types.    | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{program_stage_id}   | Contains the ID of the current program stage that triggered the rules. This can be used to run rules in specific program stages, or avoid execution in certain stages. When executing the rules in the context of a TEI registration form the variable will be empty.   | ![](/en/resources/images/admin/icon-complete.png)      | |
| V{program_stage_name} | Contains the name of the current program stage that triggered the rules. This can be used to run rules in specific program stages, or avoid execution in certain stages. When executing the rules in the context of a TEI registration form the variable will be empty. | ![](/en/resources/images/admin/icon-complete.png)      | |

> **Notes**
> 
> \* Only applies to tracker


## Differences between the Program Rules in the web and the Android version { #capture_app_pr_differences_web_android }

As the web and the Android application are currently using a different *program rule engine* there might be programs rule that work in one system and not in the other. In general terms it can be said that the Android *program rule engine* is more strict and so, some Program Rules that work in the web version of DHIS2 will fail in Android. This subsection describes the main differences and how to adapt the rules in order to have them working in both systems.

### Evaluation of type Boolean { #capture_app_pr_differences_web_android_bool }


DHIS2 web version considers the type boolean as 0 or 1 (which can be evaluated to true or false), however Android evaluates them only as true or false. While this makes possible the addition of booleans in web, it will fail in Android; in order to fix this an additional *program rule variable* is needed to transform the boolean into an number that can be operated. Check the table below for examples and possible solutions.

For the examples belows consider the following:

* yn_prv1: is a program rule variable that has been configured to get the value of a 'Yes/No' data element
* yn_prv2: is a program rule variable that has been configured to get the value of a 'Yes/No' data element
* prv_boolean_one: is a program rule variable that has been configured to get the value of a 'Yes/No' data element
* prv_boolean_two: is a program rule variable that has been configured to get the value of a 'Yes/No' data element
* prv_boolean_one_to_number: is a program rule variable with calculated value
* prv_boolean_two_to_number: is a program rule variable with calculated value
* sometimes true is used as program rule condition meaning the action is always performed
* The following acronyms are used: 
	* DE (Data Elemetn)
	* PR (Program Rule)
	* PRE (Program Rule Expression)
	* PRC (Program Rule Condition)
	* PRV (Program Rule Variable)
	* PRA (Program Rule Action)

| Program Rule Condition(s) | Program Rule Action(s) | Web version | Android version | Comment |
| ----------- | ----------- | :---: | :---: | ----- |
| d2:hasValue('yn_prv1') \|\| d2:hasValue('yn_prv2') | Assign fixed value to DE | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-complete.png) | |
| #{yn_prv1} \|\| #{yn_prv2} | Assign fixed value to DE | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-complete.png) | |
| d2:hasValue('yn_prv1') \|\| d2:hasValue('yn_prv2') | Assign value to DE: #{yn_prv1} + #{yn_prv2} + 1 | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-negative.png) | Crashes in Android  whenver a boolean is marked as the expression would result in *true*+*false*+1 |
| d2:hasValue('yn_prv1') \|\| d2:hasValue('yn_prv2') | Assign value to DE: #{yn_prv1} + #{yn_prv2} + 1 | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-negative.png) | Crashes in Android  whenver a boolean is marked as the expression would result in *true*+*false*+1 |
| PR1: #{prv_boolean_one} <br /><br />PR2: #{prv_boolean_two} <br /><br />PR3: #{prv_boolean_one} \|\| #{prv_boolean_two} | PRA1. Assign value  "1" to PRV "#{prv_bool_one_to_number}" <br /><br />PRA2. Assign value: "1" to PRV "#{prv_bool_two_to_number}" <br /><br />PRA3. Assign value to DE: "#{prv_bool_one_to_number} + #{prv_bool_two_to_number} + 1"| ![](/en/resources/images/admin/icon-negative.png) | ![](/en/resources/images/admin/icon-negative.png) | There are 2 variables for boolean, one gets the value via a PRV definition “value form DE” and the other one via a PRA. If a boolean is not marked it is counted as string instead of a number |
| Four PR to assign 1 or 0 to the booleans and an additional for the addition. Priorities go from top to bottom <br /><br />PRC1: !d2:hasValue('prv_boolean_one')  \|\| !#{prv_boolean_one} <br /><br />PRC2: d2:hasValue('prv_boolean_one') && #{prv_boolean_one}<br /><br />PRC3: !d2:hasValue('prv_boolean_two')  \|\| !#{prv_boolean_two} <br /><br />PRC4: d2:hasValue('prv_boolean_two') && #{prv_boolean_two} <br /><br />PRC5: true | PRA1: Assign value: "0" to PRV "#{prv_bool_one_to_number}" <br /><br />PRA2: Assign value: "1" to PRV "#{prv_bool_one_to_number}" <br /><br />PRA3: Assign value: "0" to PRV "#{prv_bool_two_to_number}" <br /><br />PRA4: Assign value: "1" to PRV "#{prv_bool_two_to_number}" <br /><br />PRA5: Assign value: "#{prv_bool_one_to_number} + #{prv_bool_two_to_number} + 1" to DE <br /> | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-complete.png) | There are 2 variables for boolean, one gets the value via a PRV definition “value form DE” and the other one via a PRA.

### Evaluation of numbers { #capture_app_pr_differences_web_android_numbers }


DHIS2 web version evaluate numbers in a more flexible way casting values from integer to floats and viceversa. This can lead to some issues as explained in the examples below.

#### Division of numbers

If required for a division web will cast from integer to float, however, Android take numbers as such (literally and without casting) which my end up giving unexpected results. Check the table below for examples and possible solutions.

| Program Rule Condition(s) | Program Rule Action(s) | Web version | Android version | Comment |
| ----------- | ----------- | :---: | :---: | ----- |
| true | Assign value to DE: d2:daysBetween('2020-05-13', '2020-05-17') / 3 | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-negative.png) | The user would expect the division to be calculated as 4/3 with a result of 1.3333. However, Android does not cast 4 to a float (4.0 as the web version does) so the result in Android is a pure 1 as the result of the integer division 4/3 |
| true | Assign value to DE: d2:daysBetween('2020-05-13', '2020-05-17') / 3.0 | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-complete.png) | Division results in 1.33333 in both web and Android | 


#### Using the function validatePattern

In the same way, if a DataElement of the type number is used, Android will use that value as float (including decimals) which might lead to validatePattern function not working as expected.

Consider the following:

* temperatue_prv: is a Program Rule Variable containing the value of the Data Element *temperature*.
* User inputs 38 in the Data Element.

| Program Rule Condition(s) | Program Rule Action(s) | Web version | Android version | Comment |
| ----------- | ----------- | :---: | :---: | ----- |
| !d2:validatePattern(#{temperature_prv},'\\\\{d}') | Display error if value is not 2 digits | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-negative.png) | The user would expect the program rule to NOT show an error as 38 does match the pattern. However, Android attempts to validate the pattern \\{d} against 38.0 resulting in Android displaying the error. |
| !d2:validatePattern(#{temperature_prv},'(\\\\d{2}\|\\\\d{2}\\\\.\\\\d\|\\\\d{2}\\\\.\\\\d{2})$') | Display error if value is not 2 digits | ![](/en/resources/images/admin/icon-complete.png) | ![](/en/resources/images/admin/icon-complete.png) | The regular expression used here will match both integeres and floats resulting in being properly evaluated in web and Android and not displaying an error. |

## Changes in Program Rules (as from version 2.2 of the app) { #capture_app_pr_changes }

In the version 2.2 of the application (released on August, 2020) a new rule-engine was included.  This rule-engine requires some optional and some mandatory changes to be performed on the program rules expressions in order to make it work in the new application. A list of those changes, how to detect them and how to fix them is included in the following subsections.

### Evaluation of 'd2:hasValue' { #capture_app_pr_changes_hasvalue }

#### Description

This is an optional change. *d2:hasValue* now works with both single quotes or full variable expression. The following expressions is valid: `(d2:hasValue('variable_name') and d2:hasValue(#{variable_name}))`

#### How to identify via API?

Get programRules where either the condition or the program rule action uses the d2:hasValue function.

```
https://example.org/api/programRules?fields=program[name],name,programRuleActions[data],condition&filter=programRuleActions.data:like:hasValue&filter=condition:like:hasValue&rootJunction=OR
```

```xml
<programRule name="PR01 - Check variable with hasValue(#{variable})">
<condition>d2:hasValue(#{Age in years})</condition>
<program name="JB_Testing_2.2"/>
<programRuleActions>
<programRuleAction/>
</programRuleActions>
</programRule>
<programRule name="PR01 - Check variable with hasValue('variable')">
<condition>d2:hasValue('Age in years')</condition>
<program name="JB_Testing_2.2"/>
<programRuleActions>
<programRuleAction/>
</programRuleActions>
</programRule>
```

#### How to fix it?

The example above shows how different ways of using the hasValue function will have the same effect as from version 2.2. There are no mandatory changes but have in mind that while writing new program rules being consistent might help avoiding problems.

### Evaluation of a variable { #capture_app_pr_changes_eval_var }

#### Description

This is a mandatory change. *!#{variable_name}* can only be used boolean type variables (BOOLEAN and TRUE_ONLY).

#### How to identify via API?

Get programRulesVariables with dataElements of the type NOT BOOLEAN or TRUE_ONLY

```
https://example.org/api/programRuleVariables?fields=name&filter=dataElement.valueType:!in:[TRUE_ONLY,BOOLEAN]&paging=False
```

Get all programRule.conditions
```
https://example.org/api/programRules?fields=displayName,condition&paging=False
```

Check manually (or programmatically via a script) if in the list of programRule.conditions (obtained via the second API call) any of the program rules variables (obtained via the first API call) is being used. 

For example, from the first list we get:

```xml
<programRuleVariable name="AdditionalMedication"/>
<programRuleVariable name="age"/>
<programRuleVariable name="Age in years"/>
<programRuleVariable name="AgeYears"/>
<programRuleVariable name="allergies"/>
<programRuleVariable name="apgarcomment"/>
```

And we can compare with the second list:

```xml
<programRule>
<condition>!#{Pregant}</condition>
<displayName>PR03- !#{varible_name} - BOOLEAN</displayName>
</programRule>
<programRule>
<condition>!#{Age in years}</condition>
<displayName>PR03- !#{varible_name} - NOT BOOLEAN</displayName>
</programRule>
<programRule>
<condition>#{PregnancyStatus} != 'YES'</condition>
<displayName>Pregnancy status : false</displayName>
</programRule>
```

This shows that a NON BOOLEAN variable is being used wrongly.

#### How to fix it?

Make sure that you are evaluating  BOOLEAN or TRUE_ONLY variables in your conditions. In case the program rule variable is not of that type update your program rule condition with d2:hasValue(#{variable_name}) or d2:hasValue(‘variable_name’)

In the example above the condition should change from:

```xml
<condition>!#{Age in years}</condition>
```
To:
```xml
<condition>d2:hasValue(‘Age in years’)</condition>
```

### Evaluation of texts { #capture_app_pr_changes_eval_text }

#### Description

This is a mdantory change. In program rule actions of the type ASSIGN, DISPLAY TEXT, DISPLAY KEY/VALUE PAIR, SHOW WARNING, SHOW ERROR, WARNING ON COMPLETE or ERROR ON COMPLETE if the Expression to evaluate and assign/display is a text, it must be enclosed with single quotes.

#### How to identify via API?

Get the Program Rules which actions are of type text, with something on the field data and verify their data content to find strings without quotes.

```
https://example.org/api/programRules?fields=program[name],name,programRuleActions[programRuleActionType,content,data]&filter=programRuleActions.programRuleActionType:in:[ASSIGN,DISPLAYTEXT,DISPLAYKEYVALUEPAIR,SHOWWARNING,SHOWERROR]&filter=programRuleActions.data:!null&paging=false
```

For example we can detect here an error of a text field without quotes in the first Program Rule Action while the second one is correct.

```xml
<programRule name="PR04- !#{varible_name} - BOOLEAN - Assign text without quotes">
<program name="JB_Testing_2.2"/>
<programRuleActions>
<programRuleAction>
<programRuleActionType>SHOWWARNING</programRuleActionType>
<data>embarazada</data>
<content>PR04 text with quotes is: </content>
</programRuleAction>
</programRuleActions>
</programRule>
```

```xml
<programRule name="PR04- !#{varible_name} - BOOLEAN - Assign text with quotes">
<program name="JB_Testing_2.2"/>
<programRuleActions>
<programRuleAction>
<programRuleActionType>SHOWWARNING</programRuleActionType>
<data>'embarazada'</data>
<content>PR04 text with quotes is: </content>
</programRuleAction>
</programRuleActions>
</programRule>
```

#### How to fix it?

Scan the generated list (via the suggested API calls) to find data components of the Program Rule Action where text is not quoted, then go to each of the identified Program Rules and update them.

### Concatenation of string and objects { #capture_app_pr_changes_concat }

#### Description

This is a mdantory change. In program rule actions of the type ASSIGN, DISPLAY TEXT, DISPLAY KEY/VALUE PAIR, SHOW WARNING, SHOW ERROR, WARNING ON COMPLETE or ERROR ON COMPLETE if the Expression to evaluate and assign/display is a text, it must be enclosed with single quotes (same as previous change); but, on top of that, if it requires to concatenate two strings or a combination of functions it is mandatory to use the *d2:concatenate* function.

#### How to identify via API?

Get the Program Rules which actions are of type text, with any content on the field data and verify their data content to check if in case of two or more strings (or other objects) are being joined the d2:concatenate function is used

Get the Program Rules which actions are of type text and verify their data content to find strings without quotes.

```
http://localhost:8034/api/programRules?fields=program[name],name,programRuleActions[programRuleActionType,content,data]&filter=programRuleActions.programRuleActionType:in:[ASSIGN,DISPLAYTEXT,DISPLAYKEYVALUEPAIR,SHOWWARNING,SHOWERROR]&filter=programRuleActions.data:!null&paging=false
```

For example we can detect here an error of two strings in an action without the use of d2:concatenate.

```xml
<programRule name="PR08- Assign text and variable without concatenate">
<program name="JB_Testing_2.2"/>
<programRuleActions>
<programRuleAction>
<programRuleActionType>SHOWWARNING</programRuleActionType>
<data>'Age is 10 and modulus' 'another string'</data>
<content>PR05 text without concat is: </content>
</programRuleAction>
</programRuleActions>
</programRule>
```

#### How to fix it?

Scan the generated list (via the suggested API calls) to find data components of the Program Rule Action where two or more objects are being concatenated and update them to use the d2:concatenate function.

In the example above the data should change from:

```xml
<data>'Age is 10 and modulus' 'another string'</data>
```
To:
```xml
<data>d2:concatenate('Age is 10 and modulus','another string')</data>
```
