---
layout: page
title: User Guide
---

**EduEase** is a modified version of the AddressBook Level 3 (AB3) project,
tailored specifically for private tutors with young tutees.<br>

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.<br>
   **Mac users:** Ensure you have the precise JDK version prescribed [here](https://se-education.org/guides/tutorials/javaInstallationMac.html).

1. Download the latest `.jar` file from [here](https://github.com/AY2425S2-CS2103-F09-2/tp/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your AddressBook.

1. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar eduease.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * `list` : Lists all contacts.

   * `add n/John Doe p/98765432 pp/98765433 e/johnd@example.com` : Adds a contact named `John Doe` to the Address Book.

   * `delete 3` : Deletes the 3rd contact shown in the current list.

   * `clear` : Deletes all contacts.

   * `exit` : Exits the app.

   * `note 1 a/ Needs help in multiplication of 2 digits`: Appends a note to the 1st contact in the current list.

   * `tags [t/TAG]…​` : Lists contacts based on tags.

   * `schedule` : Schedules a new session with a student.

   * `remind` : Sets a reminder for an event.
   
   * `undo` : Undoes the last command.

   * `redo` : Redoes the last known command.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the fields:**<br>

* `Name` only accepts alphabets and certain special characters such as `'`, `-`, and `/`. These special characters can only be used once. 
  * **Valid Names:** John Doe, O'Connor, Jean-Luc, Ravi S/O Lim
  * **Invalid Names:** O''Connor, -John, Mary-, S//O, 007

* `Phone Number` is based on singapore contacts and is restricted to 8 digits long. Overseas contacts will be added in the future.

</div>

### Viewing help : `help`

Shows a message explaining how to access the help page.

![help message](images/helpMessage.png)

Format: `help`


### Adding a person: `add`

Adds a person to the address book.

Format: `add n/NAME p/PHONE_NUMBER pp/PARENT_PHONE e/EMAIL  [t/TAG]…​`

* Duplicate phone numbers are allowed. In tutoring contexts with young tutees, it is common for multiple students to share the same phone number in the event they do not have a phone number or they have the same parent.

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0)
</div>

Examples:
* `add n/John Doe p/98765432 pp/98765433 e/johnd@example.com`
* `add n/Betsy Crowe t/Math e/betsycrowe@example.com p/12345678 pp/12345688 t/P3`

### Listing all persons : `list`

Shows a list of all persons in the address book.

Format: `list`

### Editing a person : `edit`

Edits an existing person in the address book.

Format: `edit INDEX [n/NAME] [p/PHONE] [pp/PARENT_PHONE] [e/EMAIL] [t/TAG]…​`

* Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
    specifying any tags after it.

Examples:
*  `edit 1 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the 1st person to be `91234567` and `johndoe@example.com` respectively.
*  `edit 2 n/Betsy Crower t/` Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name is searched.
* Partial words will be matched e.g. `Han` will match `Hans`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe`
* `find alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Deleting a person : `delete`

Deletes the specified person from the address book.

Format: `delete INDEX`

* Deletes the person at the specified `INDEX`.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd person in the address book.
* `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

### Updating a Note for a person : `note`

Updates the note of  the specified person from the address book.
The note are meant to be temporary or single-use.

Format: `note INDEX [a/ APPEND] [o/ OVERWRITE] [c/]`

* Update notes of the person at the specified `INDEX` based on parameters.
  * `a/` will append the new note with the old note with a newline.
  * `o/` will overwrite the old note with the new note.
  * `c/` will clear the note.
* If multiple additional parameter is present, priority is as follows, append > overwrite > clear.
* If no additional parameter is present, there will be no change and the old note will be shown.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​
* The note feature is designed to store and display free-form text exactly as entered by the user. Escape sequences (e.g., \n, \t, \\) are not interpreted or processed, and are instead treated as plain text.

Examples:
* `list` followed by `note 2` will show the note of the 2nd person in the address book.
* `note 1 o/ Need help in long division` will overwrite previous note.
  * Returns `Need help in long division`.
* `note 1 a/ Also need help in 7th multiplication` will append to the previous note.
  * Returns `Need help in long division\nAlso need help in 7th multiplication`
* `note 1 c/` clears the note.

### Clearing all entries : `clear`

Clears all entries from the address book.

Format: `clear`

* Requires a confirmation from user. An alert will appear for your response.
* If you prefer typing, you can press Enter again to confirm.

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Listing persons based on tags : `tags`

Shows an unique list of tags or contacts filtered based on tags. Tags are case-insensitive, `math` is treated the same as `MATH` and `MaTh`

Format: `tags [t/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip 1:**
A person can have any number of tags (including 0). <br>
:bulb: **Tip 2:** Use `list` if you want to see all contacts, `tags` does not do so.
</div>

Examples:
* `tags` shows an unique list of all tags in the address book.
* `tags t/Math` shows a unique list of persons with the `Math` tag.
* `tags t/Math t/P3` shows a unique list of persons with the tag combination of `Math` and `P3`.

About the fields:
* `Tags` should be a single alphanumeric combination.
* If users wants to combine 2 different words in a single combination, use `Pascal` or `Camel` case instead.
* **Valid Tags:** tag123, HelloWorld, helloThere, Alpha123Beta, Test1234
* **Invalid Tags:** Tag 123, Hello-World, Alpha_123, #Tag123

### Scheduling a session : `schedule`

Schedules a session with a student.

Format: `schedule n/STUDENT_NAME s/SUBJECT d/DATE t/TIME dur/DURATION`

* The date must be a future date.
* The format for date and time must be YYYY-MM-DD and HH:MM respectively.

Examples:
* `schedule n/John Doe s/Math d/2026-12-31 t/14:00 dur/1h` schedules a session with John Doe on 31st December 2026 at 2pm for 1 hour.

### Editing a session : `schedule edit`

Edits an existing session with a student.

Format: `schedule edit INDEX n/[STUDENT_NAME] s/[SUBJECT] d/[DATE] t/[TIME] dur/[DURATION]`

* Edits the session at the specified `INDEX`. The index refers to the index number shown in the sessions list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.

Examples:
*  `schedule edit 1 n/John Doe s/Science` Edits the student name and subject of the 1st session to be `John Doe` and `Science` respectively.

### Cancelling a session : `schedule cancel`

Deletes a session with a student.

Format: `schedule cancel INDEX`

### Setting a reminder: `remind`

Sets a reminder for an event at a specific time and date.

Format: `remind n/STUDENT_NAME e/EVENT d/DATE t/TIME`

* The date must be a future date.
* The format for date and time must be YYYY-MM-DD and HH:MM respectively.

  Examples:
* `remind n/John Doe e/Math exam d/2025-06-20 t/09:00` sets a reminder for John Doe having Math exam on 20th June 2025 at 9am.

### Undoing the last command : `undo`

Undoes the last command that changes the data. If there is no command to undo, the user will be informed. At the moment, the undo command only works for the contacts tab.

Format: `undo`

### Redoing the last command : `redo`

Undoes the last command that was undone. If there is no command to redo, the user will be informed. At the moment, the redo command only works for the contacts tab.

Format: `redo`

### Switching tabs : `switch`

Switches between the different tabs in the application. The tab name is case-sensitive.

Format: `switch TAB_NAME`

Example:
* `switch sessions` switches to the sessions tab.
* `switch contacts` switches to the contacts tab.
* `switch reminders` switches to the reminders tab.

### Saving the data

AddressBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

AddressBook data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the AddressBook to behave in unexpected ways (e.g., if a value entered is outside of the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</div>

### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous AddressBook home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add n/NAME p/PHONE_NUMBER pp/PARENT_PHONE e/EMAIL [t/TAG]…​` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/friend t/colleague`
**Clear** | `clear`
**Delete** | `delete INDEX`<br> e.g., `delete 3`
**Edit** | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [pp/PARENT_PHONE] [e/EMAIL] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee e/jameslee@example.com`
**Find** | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`
**List** | `list`
**Note** | `note INDEX [a/ APPEND] [o/ OVERWRITE] [c/]`<br> e.g., `note 2 a/ Need help in long division`
**Tags** | `tags [t/TAG]…​`<br>e.g., `tags`, `tags t/math`, `tags t/math t/p3`
**Schedule** | `schedule n/[STUDENT_NAME] s/[SUBJECT] d/[DATE] t/[TIME] dur/[DURATION]`<br> e.g., `schedule n/John Doe s/Math d/2022-12-31 t/14:00 dur/1h`
**Schedule Edit** | `schedule edit INDEX [n/STUDENT_NAME] [s/SUBJECT] [d/DATE] [t/TIME] [dur/DURATION]`<br> e.g., `schedule edit 1 n/John Doe s/Math d/2023-12-31 t/15:00 dur/2h`
**Schedule Cancel** | `schedule cancel INDEX`<br> e.g., `schedule cancel 1`
**Remind** | `remind n/STUDENT_NAME e/EVENT d/DATE t/TIME` <br> e.g., `remind n/John Doe e/Math exam d/2025-06-20 t/09:00`
**Undo** | `undo`
**Redo** | `redo`
**Switch** | `switch TAB_NAME` <br> e.g., `switch sessions`, `switch contacts`, `switch reminders`
**Exit** | `exit`
**Help** | `help`
