# Valance
A thin customisable PostgreSQL web interface, tuned for business applications.

Currently in research phase

## UI Components

* Valance Tables - Customisable queries reported in a table, with search, relationship traversal, and calculated columns.
* Valance Browse - Entries as customisable pages with link navigation for relationships.
* Valance Cards - Entries as customisable display cards.
* Valance Gantts - Duration based data in Gantt charts.
* Valance Pages - Connect Valance components, and external webpages, together into saveable user interfaces.
* Valance Folders - Organise stored Valance Pages in Folders.

## Tech Components

* DB: PostgreSQL
* Backend language: Javascript
* Backend framework: NodeJS
* Frontend language: Javascript
* Frontend framework: ReactJS
* Frontend tableview: react-data-grid
* Frontend gantt chart: dhtmlx-gantt (GPLv2)

## Core Features

* Authentication
* Authorization
* Database forking and sharing


## Ideas:

Users
- Shareable Components, Pages and Folders have role or user owners.
- Each user has their own Private Folder area where contents are shareable.
- Users can login with any of their assigned roles.
