
- https://wiki.postgresql.org/wiki/Don't_Do_This#Don't_use_timestamp_(without_time_zone)
- Free open-source database system that supports both relational (SQL) and non-relational (JSON) queries.
- Used as the primary database for all types of applications and its many extensions support hundreds of use cases.
- Back-end database for dynamic websites and web applications.
- Using object-oriented features of PostgreSQL, programmers can:
	- Communicate with the database servers using objects in their code.
	- Define complex custom data types.
	- Define functions that work with their own data types.
	- Define inheritance, or parent-child relationships, between tables.
- If you need to scale faster to a very large volume, PostgreSQL is a better choice.
- ```postgresql
  CREATE TABLE users (

    id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),

    email         TEXT NOT NULL UNIQUE,

    password_hash TEXT NOT NULL,

    created_at    TIMESTAMPTZ NOT NULL DEFAULT now()

);
  ```
	  - Don't use serial
		  - The serial types have some that make schema, dependency, and permission management unnecessarily cumbersome.
	  - Don't use varchar or char, just use TEXT
		  - Some databases don't have a type that can hold arbitrary long text, or if they do it's not as convenient or efficient or well-supported as varchar(n). Users from those databases will often use something like varchar(255) when what they really want is text.
	  - Don't use the timestamp type to store timestamps, use timestamptz (also known as timestamp with time zone) instead.
		  - Because there is no way for the database to know that UTC is the intended timezone for the column values.
	  - Don't use uppercase table/column names
		  - PostgreSQL folds all names - of tables, columns, functions and everything else - to lower case unless they're "double quoted".