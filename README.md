# Valance
A thin and flexible PostgreSQL web interface, designed for business applications.

Currently in research phase

## UI Components

* Valance Tables - Customisable queries reported in a table, with search, relationship traversal, and calculated columns.
* Valance Browse - Entries as customisable pages with link navigation for relationships.
* Valance Cards - Entries as customisable display cards.
* Valance Gantts - Duration based data in Gantt charts.
* Valance Pages - Connect Valance components, and external webpages, together into saveable user interfaces.
* Valance Folders - Organise stored Valance Pages in Folders.

## Tech Components

* Web User Interface - Dynamically buildable and customisable with templates.
* RestAPI - Web API elegantly aligned to the data interface requirements of Valance Tables. [Valance API](valanceAPI/README.md)

## Tech Dependencies

* DB: PostgreSQL
* DB API: node-postgres (see Row mode)
* Primary coding language: Javascript
* Backend framework: NodeJS
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
