
# Table of Contents

1.  [Objective](#org6bd4bda)
2.  [Fleeting](#orgd547bdc)
    1.  [Python](#org2e21864)
        1.  [Planning](#orgf14b0a9)
        2.  [Implementation](#orgb3cb8a0)
3.  [See Also](#orga843310)



<a id="org6bd4bda"></a>

# Objective

Via CLI receive a keyword and depending on that keyboard some message will be copied to the system clipboard. For example if I have this keywords and their corresponding messages:

-   **agree**: Yes, I agree. That sounds fine to me.
-   **busy**: Sorry, can we do this later this week or next week?
-   **upsell**: Would you consider making this a monthly donation?
    
    And I call the program with the parameter "agree" I will have in my clipboard the message "Yes, I agree. That sounds fine to me."


<a id="orgd547bdc"></a>

# Fleeting

This will chaotic because I will just write and annotate my thoughts as they come, later (if I want) I will write a cleaner version.

Another thing to consider is that I love the early return approach so I will use it. Briefly, the early return approach let me use many returns within a function to exit the function earlier, instead of using just one return statement at the end. The early return approach avoid deep nested control statements


<a id="org2e21864"></a>

## Python

I will use a [dictionary](20250111130125-python_dictionary.md) to store the relation between keywords and messages, so I will start declaring this variable somewhere (it should be inside the main function)

    text = {
        'agree': "Yes, I agree. That sounds fine to me.",
        'busy': "Sorry, can we do this later this week or next week?"
        'upsell': "Would you consider making this a monthly donation?"
    }

So the "commands" that this program will receive via CLI is "agree", "busy","upsell"


<a id="orgf14b0a9"></a>

### Planning

This program should be easy, I just receive a "command", then I would just have to validate that keyword by verifying that the "command" received is a keyword in the dictonary and then pass the corresponding text to the clipboard using the python module called [pyperclip](20250117103301-python_module_pyperclip.md) 

So, the parameters via CLI are receive via de list of sys.argv, at the index 0 is the name of the program and the parmeters start at the index 1.

-   [X] Check if the params are valid
-   [X] Select the correct text
-   [X] Copy that text to pyperclip

A possible code could be this:

    import pyperclip
    import sys
    
    def main(param1):
        text = {
            'agree': "Yes, I agree. That sounds fine to me.",
            'busy': "Sorry, can we do this later this week or next week?"
            'upsell': "Would you consider making this a monthly donation?"
        }
        if param1 not in text.keys():
            print('Invalid Keyword, try using: "agree", "busy" or "upsell"')
            return
        pyperclip.copy(text[param1])
        print(f"Copied to the clipboard the text: \"{text[param1]}\"")
        return
    
    if name == "__main__":
        if len(sys.argv)<2:
            print("Uso: python main.py <param1>")
            sys.exit
        param1 = sys.argv[1]
        main(param1)


<a id="orgb3cb8a0"></a>

### Implementation

Hopefully this wouldn't require to much for this section, just the code in the previous section.
Yep, as expected, the previous code was enough.


<a id="orga843310"></a>

# See Also

-   [Python Dictionary](20250111130125-python_dictionary.md)
-   [Python Module - sys](20250117140842-python_module_sys.md)
-   [Python - name == "<span class="underline"><span class="underline">main</span></span>"](20250117141429-python_name_main.md)

