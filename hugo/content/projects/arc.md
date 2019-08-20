---
title: Application for the ARC (Academic Resource Center)
description: An application that essentially automates the data-tracking, scheduling and attendance processes of my high school's tutoring program (200+ students).
link: https://arc-app-frontend-server.netlify.com/
code_link: https://github.com/sjhuang26/arc-app-new
code_link_2: https://github.com/sjhuang26/arc-app-frontend
timeframe: 10th grade summer
team: myself
status: ongoing
featured: true
---
{{% slide %}}
### Overview

**Background of organization:** The ARC (Academic Resource Center) is a peer-to-peer tutoring program at my high school. Upon joining the ARC in tenth grade as "tech director", I started thinking about how to design workflows for managing the data of 200+ students that the ARC handles.

**Problem:** In the ARC, each tutor needs to be scheduled with a student, and their attendance needs to be tracked. Most of this was done by hand using a paperwork system. Although the ARC used third party services to computerize attendance and volunteer-hour tracking, the user interfaces of the services were difficult for the administrators to use. Data duplication was problematic, and since there wasn't a satisfactory overview mode with statistics for each student viewable at once, adminstrators had to hand-check each student's profile one by one. All this greatly slowed down the process, with little automation.

**Solution:** I designed an application that essentially automates the ARC's tutor-scheduling and attendance tracking processes.

* The work of managing 200+ students that previously required 3-4 student volunteers is for the most part automated.
* All student data is combined into a single spreadsheet, avoiding duplicate contact entries, missing students, and other sync issues.
* The user interface has features that optimize the efficiency of the administrators.
{{% /slide %}}



{{% slide %}}
### Architecture and design

![Diagram of application architecture](/s/arc/architecture.svg)

Typescript was used as the programming language.

The top layer of the pyramid (website) provides the core user interface, while the bottom layer (spreadsheets) store the raw data.

The middle layer (Google Apps Script) is a scripting language that runs directly on the spreadsheet.

**Maintainability:** Using spreadsheets (Google Sheets) as opposed to a conventional database increases maintainability and reduces the risk of accidental data deletion. Furthermore, it is important for non-technical users to be able to access the raw data and edit it directly. While normally I would use a database, spreadsheets turn out to be more convenient.

**Error handling:** There is a communication bridge between the spreadsheet and the website that the user interacts with. If a spreadsheet operation fails, users will be notified, so that they can try again. This is an improvement over the old spreadsheets, where "silent failure" frequently occurred and students would disappear from the schedule without warning.
{{% /slide %}}



{{% slide %}}
### Design of data model
I analyzed the existing school tutoring system and modeled it as a series of objects, data structures, terminologies ("bookings ... matchings ... requests"), and statuses ("finalized ... unbooked ... unfinalized").

**Benefits:** Training and transitioning to the new system is made easier by clear analogies from pieces of old system paperwork to new system data entities. The design is such that each piece of data is present in only one location, avoiding data duplication issues and data inconsistencies that were problematic in the old system.
{{% /slide %}}



{{% slide %}}
### When a learner submits a request for a tutor...

One of the important processes the application implements is tutor-to-learner scheduling. The process begins when a learner submits a request for a tutor. The app keeps track of the necessary data and uses status trackers so the user can mark when each step is completed.

![Process when a learner submits a tutor request](/s/arc/request-process.svg)
{{% /slide %}}



{{% slide %}}
### Design of user interface

* The UI consists of windows; each operation or step gets its own window. Multiple windows can be opened at once, which is advantageous for multitasking.
* The scheduling workflow consists of three steps, one window for each step.
* A hyperlink system allows the user to jump from overview to detail view, click on a student to see detailed info about him/her, etc. 

![UI window overview](/s/arc/ui-window.svg)

**Main benefits:** The simple three-step scheduling workflow is easy to learn and keeps the scheduling process linear and organized. The hyperlink system gives the user quick access to information when it is needed, such as when contacting a student.
{{% /slide %}}



{{% slide %}}
### Tutor information UI
The user can see an overview of all tutors. New tutors' information can also be added. A similar UI exists for editing learners, requests, bookings, matchings, etc.

![Overview of all tutors](/s/arc/tutor-view-all.png)

Clicking a tutor opens a new window where their information can be edited in a standard CRUD interface. The changes made in the website are propagated to the spreadsheet.

![Detail view for a tutor](/s/arc/tutor-edit.png)
{{% /slide %}}



{{% slide %}}
### Attendance tracking UI
The attendance tracker is a simple table of all students with an expandable detail view.

![Attendance tracker](/s/arc/attendance.svg)

**Main benefits:** One page has an overview of all the important attendance info. This makes it easy to spot students with low attendance levels.

{{% /slide %}}



{{% slide %}}
### Managing the data

* Bookings and tutor-learner matchings are automatically created and managed as part of the scheduling workflow.
* Every year, new tutors and learners sign up via. electronic form, and their info is added in bulk to the data spreadsheet.

The above two processes handle most of the data. The exception is attendance data, since the attendance log is filled with hundreds of entries a day and is processed in daily chunks. Attendance data is processed like this:

1. Each tutor and learner submits their attendance data via. a form.
2. The form data goes into a spreadsheet.
3. The data is processed into an intermediate format.
4. Later, the intermediate format is reprocessed and integrated into the rest of the spreadsheet ("final format"). This data goes directly to the attendance displays.

![Attendance data processing](/s/arc/attendance-processing.svg)

Data is processed ahead of time so it doesn't need to be recalculated every time attendance info is retrieved.

**Why four steps?** The key complicating factor is that the final format needs to be compressed and optimized to make the app loads faster. While the compression could be done in a single step directly on the form data, this makes mistakes much more difficult to see. Multiple steps make the process more robust and reproducible.

**Important advantages of the four-step system:**

1. The internals of the data processing are more transparent and easier to correct. In particular, mistakes can be quickly undone.
2. There is strong backward compatibility if the form changes, because each step is separated.
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
