# FCC_RelationalDB_salon_appointment_scheduler

This is my solution for the [**Salon Appointment Scheduler**](https://www.freecodecamp.org/learn/relational-database/build-a-salon-appointment-scheduler-project/build-a-salon-appointment-scheduler)
required project for the [**freeCodeCamp's Relational Databases Certification**](https://www.freecodecamp.org/learn/relational-database/) using PostgreSQL and bash. <br />

## Contents
- [Tables](#tables)
    - [Customers](#customers)
    - [Appointments](#appointments)
    - [Services](#services)
- [Appointment Scheduler Script](#appointment-scheduler-script)   
- [Project tasks](#project-tasks)

## Tables
The database can be rebuilt by entering `psql -U postgres < salon.sql` in a terminal where the `.sql` file is.\
Rebuilding the database using this file will result in the following tables: <br />

### Customers

|customer_id <sup>1</sup>|	phone <sup>2</sup>|	name <sup>3</sup>|	
|:----------------------:|:------------------:|:----------------:|
|                        |                    |                  |

<sup>1</sup> serial, primary key, not null\
<sup>2</sup> varchar(20), unique\
<sup>3</sup> varchar(20)

[<sub>Back to top</sub>](#top)

### Appointments

|appointment_id <sup>4</sup>|	customer_id <sup>5</sup>|	service_id <sup>6</sup> | time <sup>7</sup>|	
|:-------------------------:|:-----------------------:|:-----------------------:|:----------------:|
|                           |                         |                         |                  |

<sup>4</sup> serial, primary key, not null\
<sup>5</sup> int, foreign key REFERENCES customers(customer_id)\
<sup>6</sup> int, foreign key REFERENCES services(service_id)\
<sup>7</sup> varchar(20)

[<sub>Back to top</sub>](#top)

### Services

|service_id <sup>8</sup>|	name <sup>9</sup>|
|:----------------------:|:------------------:|
|1                       | cut                |
|2                       | wash               |
|3                       | dye                |
|4                       | shave              |

<sup>8</sup> serial, primary key, not null\
<sup>9</sup> varchar(20)

[<sub>Back to top</sub>](#top)

## Appointment Scheduler Script
It can be accessed by inputting ./salon in the terminal.\
The script will print in the terminal:
> \~~~~~ MY SALON \~~~~~\
> Welcome to My Salon, how can I help you?
> 1) cut
> 2) wash
> 3) die
> 4) shave

The user should then input the number of their desired service.\
\
If the user's input is invalid (in this case, anything but 1-4), the script will print the below message and repeat the list of services:
> I could not find that service. What would you like today?

The script will then wait for a new input.

\
When a valid input is given, the script will request the user's number:
> What's your phone number?

The user should input their phone number.

\
If the script doesn't find the user's number in the [Customers](#customers) table, the script will print:
> I don't have a record for that phone number, what's your name?

The user should input their name, and the script will record the user's phone and name in the [Customers](#customers) table.\
\
After that, the script will ask:
> What time would you like your [selected service name], [customer name]?

The user should input their desired service time. \
The script will insert [customer id], [selected service id], and [selected service name] into the [Appointments](#appointments) table, print the below text, and exit.
> I have put you down for a [selected service name] at [selected service name], [customer name].

[<sub>Back to top</sub>](#top)

## Project Tasks
The goal was to create a database in PostgreSQL and a script in bash that passed the following tests \
(more details available on [**freeCodeCamp - Salon Appointment Scheduler**](https://www.freecodecamp.org/learn/relational-database/build-a-salon-appointment-scheduler-project/build-a-salon-appointment-scheduler)):
- You should create a database named `salon`
- You should connect to your database, then create tables named `customers`, `appointments`, and `services`
- Each table should have a primary key column that automatically increments
- Each primary key column should follow the naming convention, `table_name_id`. For example, the `customers` table should have a `customer_id` key. Note that there’s no `s` at the end of `customer`
- Your `appointments` table should have a `customer_id` foreign key that references the `customer_id` column from the `customers` table
- Your `appointments` table should have a `service_id` foreign key that references the `service_id` column from the `services` table
- Your `customers` table should have `phone` that is a `VARCHAR` and must be unique
- Your `customers` and `services` tables should have a `name` column
- Your `appointments` table should have a `time` column that is a `VARCHAR`
- You should have at least three rows in your `services` table for the different services you offer, one with a `service_id` of `1`
- You should create a script file named `salon.sh` in the `project` folder
- Your script file should have a “shebang” that uses bash when the file is executed (use `#! /bin/bash`)
- Your script file should have executable permissions
- You should not use the `clear` command in your script
- You should display a numbered list of the services you offer before the first prompt for input, each with the format `#) <service>`. For example, `1) cut`, where `1` is the `service_id`
- If you pick a service that doesn't exist, you should be shown the same list of services again
- Your script should prompt users to enter a `service_id`, phone number, a name if they aren’t already a customer, and a time. You should use `read` to read these inputs into variables named `SERVICE_ID_SELECTED`, `CUSTOMER_PHONE`, `CUSTOMER_NAME`, and `SERVICE_TIME`
- If a phone number entered doesn’t exist, you should get the customers name and enter it, and the phone number, into the `customers` table
- You can create a row in the `appointments` table by running your script and entering `1`, `555-555-5555`, `Fabio`, `10:30` at each request for input if that phone number isn’t in the `customers` table. 
The row should have the `customer_id` for that customer, and the `service_id` for the service entered
- You can create another row in the `appointments` table by running your script and entering `2`, `555-555-5555`, `11am` at each request for input if that phone number is already in the `customers` table. 
The row should have the `customer_id` for that customer, and the `service_id` for the service entered
- After an appointment is successfully added, you should output the message `I have put you down for a <service> at <time>, <name>.` 
For example, if the user chooses `cut` as the service, `10:30` is entered for the time, and their name is `Fabio` in the database the output would be `I have put you down for a cut at 10:30, Fabio.` 
Make sure your script finishes running after completing any of the tasks above, or else the tests won't pass

[<sub>Back to top</sub>](#top)
