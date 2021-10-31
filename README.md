# Valance
A thin and flexible PostgreSQL web interface, designed for business applications, with interfaces familiar to spreadsheet users.

The mission of Valance is to reskin PostgreSQL to be easy for technical spreadsheet users to create and configure, while providing a highly customisable and sleek web interface for non-technical users.

PostregSQL is an incredibly powerful and flexible database system, albeit a little daunting for everyone to try to learn.
Valance will never try to reinvent the wheel and will either provide intuitive interfaces, or easy to follow guides, to existing PostgreSQL features. 
When a database scales in terms of size or complexity, it will be beneficial to enlist, or build the skills of a database engineer, but this will be a natural transition, rather than a whole new development effort, that can sometimes be required when a spreadsheet is pushed to its limits.

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

## Guides

### Authentication

* For an exposed web service (XXX OAuth2 external service with encrypted JWTs - webserver to db via PostgreSQL trusted authentication).
* In a secure corporate network (XXX PostgreSQL LDAP authentication with encrypted JWTs - note exposed web service setup can also be used).
* For personal use on the same host (XXX PostgreSQL SSPI or Peer authentication.

### Authorisation (Access Restrictions)

* Restricting access to tables and columns (XXX just move columns into a restricted table that can join).
* Dividing your data into different access groups such as only allowing visibility to assigned tasks or controlling visibility on projects (XXX row level security associated with ids that divide up data across a collection of tables).

### Change logging

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

* Database forking and sharing


## Ideas:

### Users
- Shareable Components, Pages and Folders have role or user owners.
- Each user has their own Private Folder area where contents are shareable.
- Users can login with any of their assigned roles.

### Actions

Every table can have a list of actions defined that will be available to run in the UI for selected rows.
These are global for all users but may require permissions in the underlying database.
Default actions include:
* Creating a new row (if permitted).
* Deleting a row (if permitted).

Additional actions can include:
* Creating a new row in another table linked by a relationship (if permitted).
* Open a link passing in the database, the selected row identies, and an authentication token (time limited encrypted JWT) that can be placed back to perform further queries.

Actions have:
* Icon
* Name
* Description
* Authentication token validity duration.

Actions are stored in a *_valance_actions* table and admin permissions are managed on that table.

### Schema chances

