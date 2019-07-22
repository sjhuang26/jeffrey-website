---
title: ARC
description: a tutoring-scheduling app that manages ~120 tutors at my high school
link: https://arc-app-frontend-server.netlify.com/
code_link: https://github.com/sjhuang26/arc-app-new
code_link_2: https://github.com/sjhuang26/arc-app-frontend
timeframe: 10th grade summer
team: myself
status: ongoing
---
{{% slide %}}
The ARC is a peer-to-peer tutoring program at my high school. I wrote an web application that automates and manages its tutor-scheduling and attendance tracking processes.
Manual work that previously required 2-3 student volunteers is for the most part automated by the application.
{{% /slide %}}
{{% slide %}}
### Background
Upon joining the ARC in tenth grade as "tech director", I noticed that the vast majority of the scheduling of tutors was done by hand. My first solution was a spreadsheet that uses spreadsheet formulas to create a registry of tutors available for each time slot. Multiple issues soon came up:

* Coverage of only a small part of the scheduling process, with most of the scheduling still done by hand
* Very little resilience to user error

An example of a cryptic error message in the old spreadsheet:

![Example of user error in the old application](/s/arc/user-error-old.png)
{{% /slide %}}
{{% slide %}}
Because of these issues, I eventually decided to write an improved application with more functionality.

Here is the architecture:

![Diagram of application architecture](/s/arc/architecture.svg)

I used Typescript as the programming language.
{{% /slide %}}
{{% slide %}}
When designing the data model, I analyzed the existing school tutoring system and modeling it as a series of objects, data structures, terminologies ("bookings ... matchings ... requests"), and statuses ("finalized ... unbooked ... unfinalized").

Designing the app involved multiple conversations with school administrators to decide on the final feature set.
{{% /slide %}}
{{% slide %}}
Within the app, when a learner submits a request for a tutor, the following process is triggered:

![Process when a learner submits a tutor request](/s/arc/request-process.svg)

The app keeps track of things by entering data in the spreadsheet and by using status trackers/flags.
{{% /slide %}}
{{% slide %}}
The user can see an overview of all tutors. New tutors' information can also be added. A similar UI exists for editing learners, requests, bookings, matchings, etc.

![Overview of all tutors](/s/arc/tutor-view-all.png)

Clicking a tutor opens a new window where their information can be edited in a standard CRUD interface.

![Detail view for a tutor](/s/arc/tutor-edit.png)
{{% /slide %}}
{{% slide %}}
The UI consists of windows, which allow the user to view/edit information, work on a step of the tutor scheduling process, etc. Multiple windows can be opened at once.

The scheduling workflow consists of three steps. Each step opens a separate window.


![UI window overview](/s/arc/ui-window.svg)
{{% /slide %}}
{{% slide %}}
The attendance tracker is a simple table of all students with an expandable detail view.

![Attendance tracker](/s/arc/attendance.svg)
{{% /slide %}}
{{% slide %}}
### Example of data processing: attendance

The flow of data looks like this. Data is processed ahead of time so it doesn't need to be recalculated every time attendance info is retrieved.

1. Students submit attendance data via. a form, which is linked to a spreadsheet.
2. The data is processed into an intermediate format.
3. Later, the intermediate format is reprocessed and integrated into the rest of the spreadsheet ("final format").
4. The final format is directly used in the attendance displays.

![Attendance data processing](/s/arc/attendance-processing.svg)

(A similar pattern is used to handle form submissions for tutor requests.)

This two-stage data processing pattern has advantages:

1. information isn't dropped when the spreadsheet or form data is changed and recalculated
2. the internals of the data processing are more transparent and easier to correct
3. strong backward compatibility if the form changes
{{% /slide %}}
{{% learnings %}}
* I learned Typescript.
* I learned large portions of Google Apps Script, which will hopefully be helpful in future projects.
* Many elements in the app were carefully chosen for maximum extensibility in the future, without adding needless complexity to the code. I tried out multiple ideas for each of the following before settling on the final design:
	- keeping track of which sheets exist in the spreadsheet, and the type of data that each sheet contains (I modeled this as a series of resources, records, and fields)
	- designing the communication bridge between website and spreadsheet
	- error handling: ensuring that a system error results in the user being notified, not an application crash
	- writing a link system where a hyperlink to a tutor/learner can be created at any spot in the user interface
	- consuming data from forms
{{% /learnings %}}
