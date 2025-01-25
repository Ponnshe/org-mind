
# Table of Contents

1.  [Objective](#org572ccaa)
2.  [Fleeting](#orgdda1282)
    1.  [Python](#org21f667c)
        1.  [Planning](#org1a9c4f1)
        2.  [Implementation](#orge938f20)
3.  [See Also](#orgcc37bdb)



<a id="org572ccaa"></a>

# Objective

Write a regular expression that can detect dates in the DD/MM/YYYY
format. Assume that the days range from 01 to 31, the months range
from 01 to 12, and the years range from 1000 to 2999. Note that if the
day or month is a single digit, it’ll have a leading zero.
The regular expression doesn’t have to detect correct days for each
month or for leap years; it will accept nonexistent dates like 31/02/2020
or 31/04/2021. Then store these strings into variables named month, day,
and year, and write additional code that can detect if it is a valid date.
April, June, September, and November have 30 days, February has 28
days, and the rest of the months have 31 days. February has 29 days in
leap years. Leap years are every year evenly divisible by 4, except for
years evenly divisible by 100, unless the year is also evenly divisible by

1.  Note how this calculation makes it impossible to make a reasonably

sized regular expression that can detect a valid date.


<a id="orgdda1282"></a>

# Fleeting


<a id="org21f667c"></a>

## Python


<a id="org1a9c4f1"></a>

### Planning

First of all, let's do this with the text that is in the clipboard at the moment of code execution. Then, let's annote what our program has to do:

-   [X] Extract strings of this type "DD/MM/YYYY" via regex
-   Check if the date is valid:
    -   30 days: April (4), June (6), September (9), November (11)
    -   28 days February, 29 days if leap year
    -   31 days: the rest
    -   Leap years:
        -   (year % 4 \\== 0 and (year % 100 != 0 or year % 400 == 0)

1.  Create the regex to find the strings formated like DD/MM/YYYY

    Here I will use [Python Module - re](20250123205347-python_module_re.md)
    
        dates_regex = re.compile(r'''(
        ^(\d{2}) #Day
        (/)
        (\d{2}) #Month
        (/)
        (\d{4})$ #Year
        )''', re.VERBOSE)

2.  Check for if the date is valid

    I will need to iterate over the groups of the method `findall` and select the correct elements that are gonna be: 1 for the day, 3 for the month and 5 for the year. Then I will have to follow the rules above to check if the date is valid. I am going to create a function that receive three parameter day, month and year to check it.
    
        def is_leap_year(year):
            if year % 4 == 0 and (year % 100 != 0 or year % 400 == 0):
                return true
            return false
        
        def is_valid_date(day, month, year):
            if month in [4,6,9,11] and day <= 30:
                return true
            elif month == 2:
                if is_leap_year and day <= 29:
                    return true
                elif day <= 28:
                    return true
               return false
           elif day <= 31:
               return true
        
           return false
    
    Now that we have these functions we can continue with the main code
    
        for groups in dates_regex.findall(text):
            day = int(groups[1])
            month = int(groups[3])
            year = int(groups[5])
            if is_valid_date(day, month, year):
                print("/".join([day,month,year]))


<a id="orge938f20"></a>

### Implementation

There were three errors beside the syntax errors with true instead of True and false instead of False.

The first one is a logical one, in the function `is_valid_date` I never checked is the month is valid, so I had to change it to verify that month is less than 12. So this is the code for that function:

    def is_valid_date(day, month, year):
        if month > 12:
            return False
        elif month in [4,6,9,11] and day <= 30:
            return True
        elif month == 2:
            if is_leap_year(year) and day <= 29:
                return True
            elif day <= 28:
                return True
            return False
        elif day <= 31:
            return True
    
        return False

The second error is with the regex expression, I do not have to use "^" and "$" because they ensure to capture just the coincidences that occur at the start and the end of a line. For example: let's say we have the text A "The 23/02/2204 was my birthday" and the text B "23/53/3322", the code in the planning phase wont work with text A because it only capture dates if it is at the beginning and end of the line, so it would capture the date in text B. Therefore I remove the "^" and "$". This is the code:

    dates_regex = re.compile(r'''(
        (\d{2}) #Day
        (/)
        (\d{2}) #Month
        (/)
        (\d{4}) #Year
    )''', re.VERBOSE)

The third error was that I didn't know that the `join()` method just work with string iterables, so I had to change the argument and made the list contain just string elements, this could be done in two ways, I could use the `str()` function to transform the variables `day`, `month` and `year` to strings, but it wouldn't be good because the wouldn't have the "0" at the beginning if the where dates like "09", so it was better to use the groups indexes, and I put it in a variable to make it more readable. This is the code:

            date = "/".join([groups[1], groups[3], groups[5]])
    #+end_src>
    
    This is the final version:
    #+begin_src python
    import pyperclip
    import re
    def is_leap_year(year):
        if year % 4 == 0 and (year % 100 != 0 or year % 400 == 0):
            return True
        return False
    
    def is_valid_date(day, month, year):
        if month > 12:
            return False
        elif month in [4,6,9,11] and day <= 30:
            return True
        elif month == 2:
            if is_leap_year(year) and day <= 29:
                return True
            elif day <= 28:
                return True
            return False
        elif day <= 31:
            return True
    
        return False
    
    def main():
        text = pyperclip.paste()
        dates_regex = re.compile(r'''(
            (\d{2}) #Day
            (/)
            (\d{2}) #Month
            (/)
            (\d{4}) #Year
        )''', re.VERBOSE)
    
        for groups in dates_regex.findall(text):
            day = int(groups[1])
            month = int(groups[3])
            year = int(groups[5])
            date = "/".join([groups[1], groups[3], groups[5]])
            if is_valid_date(day, month, year):
                print(date)
    
    
    main()


<a id="orgcc37bdb"></a>

# See Also

-   [Python Strings](20250114133247-python_strings.md)
-   [Python List](20250111131854-python_list.md)
-   [Python Module - re](20250123205347-python_module_re.md)
-   [Python regex](20250124170551-python_regex.md)

