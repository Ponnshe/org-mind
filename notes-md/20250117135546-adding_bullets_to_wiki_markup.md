
# Table of Contents

1.  [Objective](#orgf9d9804)
2.  [Fleeting](#org9be607e)
    1.  [Python](#org0723f09)
        1.  [Planning](#org2af32d5)
        2.  [Implementation](#orgd8c40dc)
3.  [See Also](#org8b65574)



<a id="orgf9d9804"></a>

# Objective

Create a program which use the content in the clipboard to create a bullet list. In the clipboard must be a list of things, each thing should be separate by a newline character. Example, I can copy to my clipboard this:
"
Lists of animals
Lists of aquarium life
Lists of biologists by author abbreviation
Lists of cultivars
"

And to my clipboard at the there should be this:
"

-   Lists of animals
-   Lists of aquarium life
-   Lists of biologists by author abbreviation
-   Lists of cultivars

"


<a id="org9be607e"></a>

# Fleeting


<a id="org0723f09"></a>

## Python


<a id="org2af32d5"></a>

### Planning

This is the plan I have to get the content of the clipboard by using pyperclip.paste(). That string I have to split by the character "\n" using the method split("\n") to get a list of the lines. Then, to each line I should add the string "- ". Finally I have to use the join() method with the character "\n" to get the modified text and pass it to the clipboard by using pyperclip.copy().

-   [X] Get the text from paperclip **pyperclip.copy()**
-   [X] Split the text **.split("\n")**
-   [X] Modified each line **for loop**
-   [X] Join the lines **"\n".join(modified<sub>text</sub>)**
-   [X] Pass the modified text to the clipboard **pyperclip.copy(modified<sub>text</sub>)**
    
    So this could the code:

    import pyperclip
    
    def main():
        text = pyperclip.paste()
        print("Received text".upper().center(20, "="))
        print (text)
        text = text.split("\n")
        for line in text:
            line = "- " + line
        text = "\n".join(text)
    
        print("modified text".upper().center(20,"="))
        print(text)
        pyperclip.copy(text)


<a id="orgd8c40dc"></a>

### Implementation

I forgot an import thing about how python manage the for loops with the elements of a list, the variable of the for loop is a variable that saves the references, so if I want to modify the values save in the list I can not do an assignment to the variable of the for loop because I would have just been doing a change of references. However a modified to the value like via functions or method that modified the passed value and do not return another value are valid. In short, the previous code doesn't work because it doesn't save the modifications, but this code works because it saves the modifications directly to the list:
\#+begin<sub>src</sub> python
import pyperclip 

def main():
    text = pyperclip.paste()
    print("Received text".upper().center(20, "="))
    print (text)
    text = text.split("\n")
    for i in range(len(text)-1):
        text[i] = "- " + text[i]
    text = "\n".join(text)

    print("modified text".upper().center(20,"="))
    print(text)
    pyperclip.copy(text)
\#+end<sub>src</sub>>


<a id="org8b65574"></a>

# See Also

-   [Python Module - pyperclip](20250117103301-python_module_pyperclip.md)
-   [Python List](20250111131854-python_list.md)

