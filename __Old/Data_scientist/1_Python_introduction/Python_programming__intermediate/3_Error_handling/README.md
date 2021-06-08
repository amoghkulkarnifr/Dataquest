Data Scientist / Python Introduction / Python Programming: Intermediate / Error handling
========================================================================================

1. The dataset
--------------

last\_name | first\_name | birthday | gender | type | state | party
:---:|:---:|:---:|:---:|:---:|:---:|:---:|
'Bassett' | 'Richard' | '1745-04-02' | 'M' | 'sen' | 'DE' | 'Anti-Administration'
'Bland' | 'Theodorick' | '1742-03-21' | | 'rep' | 'VA' | 
'Burke' | 'Aedanus' | '1743-06-16' | | 'rep' | 'SC' |
'Carroll' | 'Daniel' | '1730-07-22' | 'M' | 'rep' | 'MD' |

The file includes these columns:

- `last_name` -- the legislator's last name
- `first_name` -- the legislator's first name
- `birthday` -- the legislator's birthday
- `gender` -- the legislator's gender
- `type` -- the chamber in which the legislator served - either Senate (`sen`) or House of Representatives (`rep`)
- `state` -- the state the legislator represents
- `party` -- the legislator's party affiliation

As you can see from the data extract, some rows contain missing values for some columns. For example, 
the `gender` and `party` columns are missing in the second row after the header row. Missing data can cause 
errors, so it needs to be dealt with.

2. Sets
-------

Sets are collection of unique objects, and it doesn't have any index associated with elements in it. 

```python
unique_animals = set(["Dog", "Cat", "Hippo", "Dog", "Cat", "Dog", "Dog", "Cat"])
print(unique_animals)           # {'Hippo', 'Cat', 'Dog'}
```

`add()` and `remove()` for adding and removing the elements to and from the set. 

The formed set can again be converted into a list by using `list()` method.

3. Exploring the dataset
------------------------

For discovering valuable things such as missing values, values that don't make any intuitive sense
or recurring themes from the data can be found out using `set` of values (as given in the following
example) -

```python
gender = []
for item in legislators:
    gender.append(item[3])

gender = set(gender)
print(gender)           # {'', 'M', 'F'}
```

4. Missing values
-----------------

Some datasets can have misssing values which can be dealt with - 

- Removing the data point
- Initializing the data point with a default value
- Initializing the data point with a calculated value
- Use analysis techniques that work with missing data.

5. Parsing birth years
----------------------

Change format of the value of birthday from `"YYYY-MM-DD"` to `["YYYY", "MM", "DD"]`. Use `split()`.

```python
birth_years = []
for row in legislators:
    birthday = row[2]
    parts = birthday.split("-")
    birth_years.append(parts[0])
```

6. Try/Except blocks
--------------------

Basics of try-except blocks.

```python
try:
    float("hello")
except Exception:
    print("Error converting to float.")
```

7. Exception instances
----------------------

When the Python interpreter creates an exception, it actually creates an instance of the `Exception` class (!).

```python
try:
    int('')
except Exception as exc:
    print(type(exc))            # <class 'ValueError'>
    print(str(exc))             # invalid literal for int() with base 10: ''
```

8. The `pass` keyword
---------------------

The `pass` keyword is used when you don't want to include anything special in the body of `except` block. It essentially
is a dummy statement for a custom `except` block.

9. Convert birth years to integers
----------------------------------

Append the birthyear in `int` to the row, and if it is `''` then append 0.

```python
birthday_col = 2
birth_year_col = 0
for legislator in legislators:
    birth_year = 0
    birthday = legislator[birthday_col]
    date = birthday.split('-')
    try:
        birth_year = int(date[birth_year_col])
    except:
        pass
    legislator.append(birth_year)
```

10. Fill in years without a value
---------------------------------

Years which are set to 0, are set to the years of the last row.

```python
last_value = 1
for legislator in legislators:
    if legislator[7] == 0:
        legislator[7] = last_value
    last_value = legislator[7]
```

`last_value` keeps track of the previous row's column no 7 in `legislator`, and sets it to the next occurrance of `0`
in the same column.
