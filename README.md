# Valance
A thin and flexible PostgreSQL web interface, designed for business applications, with interfaces familiar to spreadsheet users.

The mission of Valance is to reskin PostgreSQL to be easy for technical spreadsheet users to create and configure, while providing a highly customisable and sleek web interface for non-technical users.

PostregSQL is an incredibly powerful and flexible database system, albeit a little daunting for everyone to try to learn.
Valance will never try to reinvent the wheel and will either provide intuitive interfaces, or easy to follow guides, to existing PostgreSQL features. 
When a database scales in terms of size or complexity, it will be beneficial to enlist, or build the skills of a database engineer, but this will be a natural transition, rather than a whole new development effort, that can sometimes be required when a spreadsheet is pushed to its limits 

Currently in research phase.

---
XXX - Clean up everything below this line

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
