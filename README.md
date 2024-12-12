# Actifai Engineering Takehome

## Introduction

You are an Actifai backend engineer managing a database of our users - who are call center agents - and the sales that
the users place using our application.

The database has 4 tables:

- `users`: who are the users (name, role)
- `groups`: groups of users
- `user_groups`: which users belong to which groups
- `sales`: who made a sale, for how much, and when was it made

The front-end team has decided to build an analytics and reporting dashboard to display information about performance
to our users. They are interested in tracking which users and groups are performing well (in terms of their sales). The
primary metric they have specified as a requirement is average revenue and total revenue by user and group, for a given
month.

Your job is to build the API that will deliver data to this dashboard. In addition to the stated requirements above, we
would like to see you think about what additional data/metrics would be useful to add.

At a minimum, write one endpoint that returns time series data for user sales i.e. a list of rows, where each row
corresponds to a time window and information about sales. When you design the endpoint, think  about what query
parameters and options you want to support, to allow flexibility for the front-end team.

## Codebase

This repository contains a bare-bones Node/Express server, which is defined in `server.js`. This file is where you will
define your endpoints.

## Getting started

1. Install Docker (if you don't already have it)
2. Run `npm i` to install dependencies
3. Run `docker-compose up` to compile and run the images.
4. You now have a database and server running on your machine. You can test it by navigating to `http://localhost:3000/health` in
your browser. You should see a "Hello World" message.


## Help

If you have any questions, feel free to reach out to your interview scheduler for clarification!
## API Documentation

### Get Total and Average Revenue by User in a Given Month

**Endpoint**  
`GET /api/sales/users?month={YYYY-MM}&userId={userId}`

**Description**  
Fetches the total revenue, average revenue, and the number of transactions for a specific user within a given month.

#### Parameters:
- `month` (query parameter): The month for which to retrieve the revenue data, in the format `YYYY-MM`. Example: `2021-01`.
- `userId` (query parameter): The unique identifier of the user whose revenue data is being fetched.

#### Response:
- **Status Code**: 200 OK  
- **Content**:
    ```json
    [
        {
            "user_id": 2,
            "user_name": "Bob",
            "total_revenue": "344014",
            "average_revenue": "26462.615384615385",
            "transactions": "13",
            "time_window": "2021-01-01T00:00:00.000Z"
        }
    ]
    ```

#### Fields:
- `user_id`: The unique ID of the user.
- `user_name`: The name of the user.
- `total_revenue`: Total revenue generated by the user during the specified month.
- `average_revenue`: The average revenue per transaction for the user during the specified month.
- `transactions`: The number of transactions made by the user.
- `time_window`: The month for which the data is retrieved.

---

### Get Total and Average Revenue by Group in a Given Month

**Endpoint**  
`GET /api/sales/groups?month={YYYY-MM}&groupId={groupId}`

**Description**  
Fetches the total revenue, average revenue, and the number of transactions for a specific sales group within a given month.

#### Parameters:
- `month` (query parameter): The month for which to retrieve the revenue data, in the format `YYYY-MM`. Example: `2021-01`.
- `groupId` (query parameter): The unique identifier of the sales group whose revenue data is being fetched.

#### Response:
- **Status Code**: 200 OK  
- **Content**:
    ```json
    {
        "group_id": 1,
        "group_name": "Northeast Sales Team",
        "total_revenue": "10579182",
        "average_revenue": "26251.071960297767",
        "transactions": "403"
    }
    ```

#### Fields:
- `group_id`: The unique ID of the sales group.
- `group_name`: The name of the sales group.
- `total_revenue`: Total revenue generated by the sales group during the specified month.
- `average_revenue`: The average revenue per transaction for the group during the specified month.
- `transactions`: The number of transactions made by the group during the specified month.
