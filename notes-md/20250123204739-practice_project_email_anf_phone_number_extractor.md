
# Table of Contents

1.  [Objective](#org445e43c)
2.  [Fleeting](#org60a1bc1)
    1.  [Python](#orgf7e257f)
        1.  [Planning](#orgc99a27f)
        2.  [Implementing](#org10480f5)
3.  [See Also](#org227b03d)



<a id="org445e43c"></a>

# Objective

Say you have the boring task of finding every phone number and email
address in a long web page or document. If you manually scroll through
the page, you might end up searching for a long time. But if you had a
program that could search the text in your clipboard for phone numbers
and email addresses, you could simply press CTRL-A to select all the text,
press CTRL-C to copy it to the clipboard, and then run your program. It
could replace the text on the clipboard with just the phone numbers and
email addresses it finds.


<a id="org60a1bc1"></a>

# Fleeting


<a id="orgf7e257f"></a>

## Python


<a id="orgc99a27f"></a>

### Planning

So for this project I will need to do the next things:

1.  Get the text from the clipboard

    This action is pretty simple, I will just have to use function `paste()` of the [Python Module - pyperclip](20250117103301-python_module_pyperclip.md). and save it in a variable. This code should work just fine.
    
        import pyperclip
        text = pyperclip.paste()

2.  Extract the emails from the text

    Now for this I will have to use the  [Python Module - re](20250123205347-python_module_re.md), create a regex group for the standard way of a email addres.
    
    An email addres is formed by:
    
    -   Username: It can be a combination of these *lowercase*, *uppercase*, *numbers*, *a dot*, *underscore*, *percent sign*, *plus sign* or *hyphen*
    -   The *@* character
    -   Domain name: *letters*, *numbers*, *periods*, *hyphens*
    -   Top level domain: *dot* and two to four letters
        
        So I will need to create a regex group like this:
    
        import re
        email_regex = re.compile(r'''(
        [a-zA-Z0-9._%+-]+  #username, I will find one or more of that group of characters
        @
        [a-zA-Z0-9.-]+   #domain name
        (\.[a-zA-Z]{2,4}) #Top level domain
        )
        ''', re.VERBOSE)

3.  Extract the phone numbers from the text

    For the phone numbers I will follow the next conventions:
    
    -   An optional area code, three numbers
    -   Separator
    -   Three numbers
    -   Separator
    -   Four numbers
    -   An optinal Extension
        
        The separator can be an space, hyphen or a dot. And the extension can be written after many spaces and have as a suffix ext, ext., x some space and 2 to 5 numbers.
    
    So this could be the regex:
    
        phone_regex = re.compile(r'''(
        (\d{3}|\(\d{3}\))? #Optional area code
        (\s|-|\.)? #Optional separator
        (\d{3})  #First three digits
        (\s|-|\.) #Separator
        (\d{4})  #Last four digits
        (\s*(ext|ext.|x)\s*(\d{2,5}))? #Extension
        )
        ''', re.VERBOSE)

4.  Paste the phones and emails in the clipboard

    To paste the information in the clipboard I will first need to get all the coincidences for the regex from the text. Then I will have to format them to create a text and paste that text in the clipboard. So I will do this:
    
        matches = []
        for groups in email_regex.findall(text):  #Fot the email addresses
            matches.append(groups[0])
        
        for groups in phone_regex.findall(text):
            phoneNum = "-".join(groups[1]+groups[3]+groups[5])
            if groups[8] != "":
                phoneNum += " x" + groups[8]
            matches.append(phoneNum)
        
        if len(matches) > 0:
            pyperclip.copy("\n".join(matches))
            print('Copied to clipboard:')
            print('\n'.join(matches))
        else:
            print('No phone numbers or email addresses found.')


<a id="org10480f5"></a>

### Implementing

During the iteration for the phone numbers I forgot how the join method works and I pass it a string instead of a list.
The code end up like this:

    import pyperclip
    import re
    
    text = str(pyperclip.paste())
    
    email_regex = re.compile(r'''(
    [a-zA-Z0-9._%+-]+ #username
    @
    [a-zA-Z0-9.-]+ #domain name
    (\.[a-zA-Z]{2,4}) #Top level domain
    )''', re.VERBOSE)
    
    phone_regex = re.compile(r'''(
    (\d{3}|\(\d{3}\))? #Area code
    (\s|-|\.)? 
    (\d{3}) #Three first numbers
    (\s|-|\.)
    (\d{4}) #Last four numbers
    (\s*(ext|ext\.|x)\s*(\d{2,5}))? #Extension
    )''', re.VERBOSE)
    
    matches = []
    for groups in email_regex.findall(text):
        matches.append(groups[0])
    
    for groups in phone_regex.findall(text):
        phoneNum = '-'.join([groups[1],groups[3],groups[5]])
        if groups[8] != "":
            phoneNum += " ext." + groups[8]
        matches.append(phoneNum)
    
    if len(matches) > 0:
        pyperclip.copy("\n".join(matches))
        print("Phone numbers and emails copied to the clipboard")
        print("\n".join(matches))
    else:
        print("No matches")


<a id="org227b03d"></a>

# See Also

-   [Python List](20250111131854-python_list.md)
-   [Python regex](20250124170551-python_regex.md)

