---
description: Development practices at Origin Protocol
---

# Engineering Handbook

## **Prioritisation**

Prioritization is the most important thing we do when building products and it is important that we are always trying to work on the tasks that will have the most impact. This is more difficult when products are not yet accepting public users or a product has not found product market fit so extra attention should be paid in those situations.

In general, prioritization should be mostly managed by PMs. Engineers should be free to implement without needing to think about priority because that is how they are most productive. Engineers are free to move between tasks or provide guidance to PMs if they believe some prioritization is not as effective as it could be.

## Code Hygiene

Code formatting should always be delegated to an opinionated formatter with its standard ruleset \(e.g. `prettier` for JavaScript, or `black` for Python\). Line lengths should be limited to 80 characters if this is not the standard. ****This avoids the need to write and maintain style guides.

### Code Reviews

Code that leaves the project in a better state should always be accepted. 

Reviewers should ensure that changes are not more complex or generic than is required by the functionality being implemented. Code changes should only be addressing what needs to be done now, not what might need to be done in the future. It is still a useful exercise to consider what might need to be done in the future and implement accordingly, provided it is a case of code differently rather than code more.

Prefix any comments on code reviews that are minor in nature with `nit:`

### Commenting

Comments should be used to explain the "why". Why does this piece of code exist and why was it implemented this way? This is information that cannot be well captured in the code itself.

Comments should not be used to explain what code is doing. The code should do that. If reading the code does not provide an explanation of what it is doing it should be rewritten in a simpler form. Exceptions are particularly complex pieces of code that can't be rewritten in a form that would make it more readable.

Keep in mind that comments that have become outdated or comments that are otherwise confusing are more harmful to clarity than no comments at all.

### Testing

Tests can be useful in the right context, but we don't require all new code to be accompanied by a full set of tests. Tests are more code, and all code incurs a cost \(whether it be technical debt or or maintenance costs\).

Whether or not to write tests is up to the individual engineer, but here are some rules of thumb:

* Anything high risk, e.g. transfer of currency or something with security implications.
* When a non-obvious bug has been fixed and a test would serve well as a guard against regression and as documentation. It is useful in this case to write the test prior to implementing the fix.
* For core components to allow for faster iteration.

## **Data-oriented Design**

> Show me your flowcharts and conceal your tables, and I shall continue to be mystified. Show me your tables, and I won’t usually need your flowcharts; they’ll be obvious. -- Fred Brooks

Great care should be taken in the data design when changing an existing project or spinning up new projects. It is the most difficult part of a software system to change, and most projects that mature even slightly will end up with multiple applications interacting with the data schema. Further, our engineers move between products and the data design is a critical piece in gaining understanding of a new codebase.

### Databases

We prefer PostgreSQL everywhere. Although SQLite can be handy for quick prototyping, it should never be used as a replacement for PostgreSQL in development or testing due to it not being a fully featured SQL compliant database, and because it can behave differently to PostgreSQL in certain situations.

Database schemas should always be fully source controlled. Any changes should be done via a migration and committed \(yes, even the creation of indexes\). Some additional rules of thumb for dealing with databases:

* Every table has an autoincrement column named `id` 
* Every table has audit columns `created_at` and `updated_at`
* Table names, column names, constraints and indexes only ever use lowercase and snake case. Snake case is faster to read than camel case and it plays nicely with command line tools like `psql`
* Avoid JSON or JSONB column types. If one of these types is being used the structure should be fully documented in comments.

### Things that aren't databases

As a blockchain company, we are often building products that have no centralized component like a PostgreSQL database. In the case of large JSON structures the format should be well documented in comments.

### Example data

All projects should have example data to eliminate the requirement of manually populating data as the first step to developing a feature.

## 





