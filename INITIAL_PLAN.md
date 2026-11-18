Reading Tracker — Project Plan
Project goal
Build a small web app for tracking books and reading progress. This is a learning project, especially for someone new to full-stack development. The goal is to understand how C#, web pages, HTTP requests, and a database fit together—not to create a production-scale Goodreads clone.

We will build the simplest useful version first, then decide together which features to add.

Proposed tech stack (please discuss)
Part	Proposal	Why
Language	C#	Learn and practice C#
Web framework	ASP.NET Core	Web development with .NET
UI	Razor Pages	HTML and page-handling C# stay close together; beginner-friendly
Database	SQLite	Works locally without running a database server
Database access	Entity Framework Core	Practice entities, queries, and migrations
Styling	Simple CSS or Bootstrap	Keep attention on application behavior
Tests	xUnit	Practice testing important behavior
Collaboration	Git and GitHub pull requests	Learn branches, code review, and teamwork
MVC versus Razor Pages: Both would work. I recommend Razor Pages for the first project because there are fewer moving parts to learn at once. If we both prefer MVC, we can choose that before coding.

Open decision: accounts in the MVP?
Option A — No accounts (recommended for learning): One shared/local book collection. We can finish CRUD first and add user accounts later. Do not publicly deploy an unauthenticated app that lets anyone edit or delete records.

Option B — Accounts from the beginning: Each person signs in and manages their own books using ASP.NET Core Identity. This is a useful learning exercise, but adds authentication, authorization, ownership checks, and more testing before basic CRUD is complete.

Decision: [ ] A — No accounts [ ] B — Accounts from the start

If we choose A but want accounts later, we should avoid assuming the app will permanently have only one user. However, we do not need to build authentication infrastructure in advance.

Other things to decide together: project/repository name, Razor Pages versus MVC, and how much AI assistance we are comfortable with.

MVP scope
The first release lets someone:

Add a book.
View the book list and an individual book.
Edit a book.
Delete a book after confirmation.
Set a reading status and update their current page.
Suggested book fields
Field	Notes
ID	Database-generated identifier
Title	Required
Author	Required
Description	Optional
Total pages	Optional, positive if provided
Current page	Starts at 0; cannot be negative
Reading status	Want to Read, Reading, Completed, Did Not Finish
Date added	Set by the application
Date started / finished	Optional
Keep the MVP to a single Book entity unless we choose user accounts from the outset. Tags, authors as separate entities, reviews, and reading sessions can wait.

Basic rules to discuss and test
Title and author cannot be blank.
Current page cannot exceed total pages when total pages are known.
Finish date cannot precede start date when both are supplied.
Decide whether marking a book Completed automatically sets its current page to the total.
Invalid form submissions should show useful validation errors without losing entered data.
Nonexistent book IDs should show an appropriate not-found response.
Delete must require a confirmation POST; viewing a link must never delete data.
If we add accounts, every book read/write operation must be scoped to its owner.
Pages
Page	Purpose
/	Simple introduction or overview
/Books	List books and their status/progress
/Books/Create	Add a book
/Books/Details/{id}	Read one book's details
/Books/Edit/{id}	Update book details/progress
/Books/Delete/{id}	Confirm and delete a book
Avoid a separate JavaScript SPA, REST API, or complicated architecture in the MVP. Server-rendered pages are sufficient.

Milestones
Each milestone should produce a working, reviewable change. We can create GitHub issues from these once the repository exists.

1. Repository and running app
 Create the repository and invite collaborators.
 Create an ASP.NET Core Razor Pages application.
 Run it locally and change the homepage text.
 Make a commit, push a branch, and open a small pull request.
Done when: Both collaborators can clone, build, and run the app. Explain what .cshtml and .cshtml.cs are for.

2. Book model and SQLite
 Define Book and its reading status enum.
 Add an EF Core DbContext and configure SQLite.
 Create and apply the first migration.
 Inspect the resulting database/table.
Done when: The app starts and the database schema exists.

3. List and view books (Read)
 Display all books with an empty-state message.
 Add a details page for an individual book.
 Handle an unknown book ID.
Learn: HTTP GET, Razor syntax, dependency injection, LINQ, async database queries.

4. Add books (Create)
 Build an HTML form.
 Bind and validate its fields.
 Save a book with EF Core.
 Redirect after a successful POST.
Learn: Forms, HTTP POST, model binding, validation, and Post/Redirect/Get.

5. Edit books (Update)
 Load existing values into an edit form.
 Validate changes and save them.
 Avoid updating fields the user is not allowed to control.
Learn: Route IDs, updates, input models, and handling invalid input.

6. Delete books (Delete)
 Show the book and ask for confirmation.
 Delete only after a POST.
 Redirect to the list and handle missing books.
Done when: All four CRUD operations work end to end.

7. Reading progress
 Update current page and reading status.
 Show progress as a percentage only when total pages are known and valid.
 Decide how started/completed dates behave.
 Add tests for progress calculation and validation edge cases.
Done when: A reader can track an unfinished book through completion.

8. Polish and verification
 Add sensible navigation and basic responsive styling.
 Test CRUD manually from a fresh database.
 Add targeted automated tests for business rules and important web flows.
 Document local setup and migration commands in README.md.
 Agree whether the MVP is finished before adding features.
Later ideas — not MVP requirements
Book ratings and reviews
Search, sorting, and filtering
Genres or tags
Reading sessions (date, pages read, minutes spent)
Reading goals and statistics
Cover images and optional ISBN lookup
Import/export
User accounts, if deferred
Deployment after authentication/access control decisions
How we'll work together
Work in small features and use GitHub issues/branches/pull requests.
Prefer the learner implementing features, with discussion and code review from the more experienced collaborator.
Review the reasoning behind a change, not just whether it compiles.
Use official docs, experimentation, and debugging as learning tools.
Agree on AI usage before starting: none; explanations/reviews only; documentation only; or implementation assistance with careful human review. No one should feel pressured into a level of AI use they do not want.
Keep milestones flexible. If a concept takes longer to understand, that's fine.
First conversation / kickoff checklist
 Choose Razor Pages or MVC.
 Choose accounts now or later.
 Decide on AI use.
 Confirm both developers can run the .NET SDK and use Git/GitHub.
 Create the repo and tackle Milestone 1.
The aim is a small finished project we both understand. We can always make it fancier later.
