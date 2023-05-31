# Park Search Engine

For this assignment, we'll be building a search engine for the park data collected in the last assignment.

Our data has been cleaned up & normalized, and imported into a SQLite database.

You can use the `sqlite3` command line tool to explore the database & run queries against it.

Here's an example of viewing the tables and their schemas:

```bash
$ sqlite3 data/parks.db
SQLite version 3.37.0 2021-12-09 01:34:53
Enter ".help" for usage hints.
sqlite> .tables
park_times parks
sqlite> .schema parks
CREATE TABLE parks (
        id INTEGER PRIMARY KEY,
        name TEXT,
        address TEXT,
        history TEXT,
        description TEXT,
        url TEXT,
        tokens TEXT,
        latitude REAL,
        longitude REAL
    );
sqlite> .quit
```

In the `parks_search` directory, you'll find a simple web interface for searching the database built using Flask.

* `parks_search/search.py` contains the search functionality.  You will need to implement this file.
* `parks_search/app.py` contains the Flask app.  You do not need to modify this file.
* `parks_search/templates/index.html` contains the HTML template for the web interface.  You do not need to modify this file.

## Warm Up Part 1

Before you start on this assignment, it is recommended that you get comfortable with writing SQL queries with the following exercises:

1. Find the name of all parks that start with the letter 'W'.

2. Find the name and address of all parks within 60637.

3. Find the name and address of all parks that are open on Wednesdays at 9pm (represented as 2100).

4. Find the name and address of all parks that contain the keyword "basketball".

5. Find the name, address, and description of all parks that are open at 5am on a Saturday (represented as 0500) that contain the keyword "reformer".

Place these results inside ``warmup1.sql``. These will not be
graded. However, they provide evidence that you attempted to complete the warmup exercises.

(Note: you will need to use `JOIN` to complete these queries as they span tables.)

## Warm Up Part 2

The built-in library `sqlite3` is a Python library that allows you to interact with a SQLite database.

You'll use the following functions:

`sqlite3.connect(filename)`:  Opens a connection to the database file `filename`. Returns a `Connection` object.

`connection.cursor()`: Returns a `Cursor` object that can be used to execute queries.

`cursor.execute(query, args)`: Executes the SQL query `query` on the database. The query may have placeholders indicated by `?` within the string.  If there are placeholders, `args` will be used to fill in the values. `args` should be a tuple.

`cursor.fetchall()`: Returns a list of all the results of the query.  Should be called after a `SELECT` query via `cursor.execute()`.

`connection.close()`: Closes the connection to the database.

Example:

```python
import sqlite3

connection = sqlite3.connect('data/parks.db')
connection.row_factory = sqlite3.Row        # remember to include this as discussed in class
cursor = connection.cursor()
# each ? in the query is replaced by the corresponding element in the tuple
cursor.execute('SELECT * FROM parks WHERE id = ?', (1,))
print(cursor.fetchall())
connection.close()
```

For this part of the warm-up, translate your SQL queries from the previous part into Python code using the `sqlite3` library. Be sure all of your queries are parameterized.  Place these results inside ``warmup2.py``. (These will not be graded either.)

Note: The path used (`data/parks.db`) assumes you are running from the root of the repository.  If you are running from a different directory, you will need to adjust the path accordingly.  (e.g. if you are running from within `parks_search`, you would use `../data/parks.db`.)

## Distance Function

We have provided a function `haversine_distance` in `db.py` that calculates the distance between two points on the Earth.

This will be used in your search engine to calculate the distance between a park and a given location.

You can arrange to have `sqlite3` call a Python function while processing a query. This is done by registering the function with the database connection using `connection.create_function`.

`create_function` requires a name for the function, a number of arguments, and a function object:

```python
import sqlite3

connection = sqlite3.connect('data/parks.db')
connection.create_function('haversine_distance', 4, haversine_distance)

cursor = connection.cursor()
cursor.execute('SELECT haversine_distance(?, ?, latitude, longitude) AS distance FROM parks', [41.8781, -87.6298])
```

You'll use this function to implement the `distance` search term, that means you will need to register it with the database connection in `search.py`.

(Note: A handful of parks could not be geocoded and have a lat & lon of `0.0`, don't worry about these not showing up in your results.)

## Web Interface

There's a web interface for searching the database built with Flask.

You can run it via:

```bash
FLASK_DEBUG=1 poetry run python -m parks_search.app
```

or if you prefer:

```bash
$ poetry shell
(venv-xyz123) $ FLASK_DEBUG=1 python3 -m parks_search.app
```

Doing so will start a web server.

`FLASK_DEBUG=1` will enable debug mode, which will automatically reload the server when you make changes to the code. This is optional, but it will make development much easier.

If it runs successfully you will see output like:

```
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:8719
 * Running on http://128.135.164.171:8719
Press CTRL+C to quit
```

If you are running on a CS Linux server, the second URL is the one you'll want to visit in a web browser.  (The exact URL will differ.)  If you are running locally you'll just see the 127.0.0.1:port URL, and can use that one.

If you get an error about a port already being used, just try running again, the server selects a random port. As noted in the output, you will use **Ctrl-C** to quit the server at any time.

Note: It will be helpful to run this in its own window, as it needs to stay running while you interact with the server.

When the user enters a search term, the web interface will call the `parks_search` function in `search.py`. The possible search terms are:

* `name`: searches by name (string)
* `query_terms`: searches tokens (list of strings)
* `zip_code`: searches address (string)
* `open_at`: a tuple with two elements (`day`, and `time`)
  * `day`: A day of the week (string) to check if the park is open.
  * `time`: A time (0000-2359) to check if the park is open.
* `near`: a tuple with three elements (`latitude`, `longitude`, and `distance`)
  * `latitude`: The latitude of the point to check distance from. (float)
  * `longitude`: The longitude of the point to check distance from. (float)
  * `distance`: The maximum distance (in miles) to search. (float)

Some tips:

* If `name` is provided, the park's name must *start with* the provided string.
* If `query_terms` is provided, the park's tokens must contain *all* of the provided terms. Tokens must match exactly, so "pickle" will not match "pickleball."
* If `zip_code` is provided, the park's address must contain the provided zip code.
* If `open_at` is provided, the park must be open at that time on that day. Consider the park's hours of operation inclusive (e.g. if a park is open from 9am-5pm, it is open *at* 9am and 5pm but not 8:59am or 5:01pm).
* A park only matches if *all* of the provided search terms match.

## Task

Your task is to implement the search functionality in `search.py`.

Your function must return a list of parks that match the provided search terms, for example:

```python
search_terms = {
    'query_terms': ['basketball'],
    'zip_code': '60622',
}
parks = search.search_parks(search_terms)
# parks will now contain the 3 parks in 60622 that contain the keyword "basketball"
```

If the search returns no results, an empty list will be returned.

Your function will need to query `data/parks.db` to find the matching parks.

### Tips

**Example Query**

If you received the parameters:

```python
search_terms = {
    'name': 'Washington',
    'query_terms': ['basketball'],
    'day': 'wed',
    'time': '0900',
}
```

An example query might look like:

```sql
SELECT
     parks.name, parks.description, parks.history, parks.address, parks.url,
     park_times.day, park_times.open_time, park_times.close_time
FROM 
    parks JOIN park_times ON parks.id = park_times.park_id
WHERE
    day = 'wed'
    AND open_time <= '0900'
    AND close_time >= '0900'
    AND name LIKE 'Washington%' 
    AND tokens LIKE '% basketball %';
```

(Spacing is just for readability.)

**str.join**

The `str.join` method is useful for joining a list of strings together with any other string as a separator. For example:

```python
>>> ', '.join(['a', 'b', 'c'])
'a, b, c'
```

You may want to use this to join together pieces of your SQL query.

**What attributes to include?**

The attributes included in the returned park objects will
depend on the search terms provided.

Always include the following attributes from the parks table:

* `name`
* `address`
* `description`
* `history`
* `url`

If the search terms include `day` and `time`, include the following attributes from the park_times table:

* `day`
* `open_time`
* `close_time`

If the search terms include `latitude`, `longitude`, and `distance`, include a `distance` field that is the distance from the provided point.

* `distance` (as computed by `haversine_distance`)

**UI Note**

There are some fields in the UI that must be provided together:

* day & time - if one is provided, the other must be provided
* latitude, longitude, & distance - if one is provided, the other two must be provided

**SQL Injection**

Your code must be safe from SQL injection.  You should not use string formatting to build your SQL queries.  Instead, use the `?` placeholder syntax.  Not doing so will result in a "major" error deduction when we grade your code.

## Testing & Debugging

Tests are provided in `tests/test_search.py`.

You can also debug your code using IPython and hand-constructed
input dictionaries.  This may be easier than using the web interface.

We will only provide help debugging your code if there is evidence in your repository that you attempted the warm up exercises.
