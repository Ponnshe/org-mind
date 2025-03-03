
# Table of Contents

1.  [Objective](#org6297d6c)
2.  [Fleeting](#org1578a20)
    1.  [Python](#orgff0c4ec)
        1.  [Planning](#org7607f9e)
        2.  [Implementation](#orgc3b49c5)



<a id="org6297d6c"></a>

# Objective

Pig Latin is a silly made-up language that alters English words. If a word
begins with a vowel, the word yay is added to the end of it. If a word
begins with a consonant or consonant cluster (like ch or gr), that
consonant or cluster is moved to the end of the word followed by ay.
Let’s write a Pig Latin program that will output something like this:
Enter the English message to translate into Pig Latin:
My name is AL SWEIGART and I am 4,000 years old.
Ymay amenay isyay ALYAY EIGARTSWAY andyay Iyay amyay 4,000 yearsyay oldyay.


<a id="org1578a20"></a>

# Fleeting


<a id="orgff0c4ec"></a>

## Python


<a id="org7607f9e"></a>

### Planning

First I will need to ask the user for an input. Then I will need to split the input. After that I will have to work word for word, use a for loop.

Each word will have to get strip of the non alfa characters, I will do this by using the `isalpha()` method, if a character is not alfa I will have to save it in some auxiliar string, I will do this for prefix and suffix.

Then, I will have to remember if the word is in upper or if it is a title. After that I will "strip" the consonant characters at the beginning of the word. If there is consonant characters at the beginning of the word I will add them at the end of the word plus the "ay" ending. If there are not consonant characters at the beginning of the word I will just add the "yay" ending to the word.

-   [X] Ask for an input
-   [X] Split the input
-   [X] Strip the non-alpha characters for each word
-   [X] "strip" the consonants at the beginning of the word
    -   [X] If there are consonants, move them at the end of the word plus the "ay" ending
    -   [X] If there are not consonant, add the "yay" ending
        
        So this could be a code:
        
            def main():
                text = input("Ingrese el texto a traducir: \n")
                text = text.split()
                pig_latin = []
            
                if not text:
                    return
            
                for word in text:
                    prefix_non_alpha = ''
                    while not word[0].isalpha():
                        prefix_non_alpha += word[0]
                        word = word[1:]
                    if len(word) == 0:
                        pig_latin.append(prefix_non_alpha)
                        continue
            
                    suffix_non_alpha = ''
                    while not word[-1].isalpha():
                        suffix_non_alpha += word[-1]
                        word = word[0:-1]
            
                   is_upper = word.isupper()
                   is_title = word.istitle()
            
                   consonant_prefix= ''
                   word = word.lower()
            
                    while len(word) >0 and not word[0] in "aeiou":
                        consonant_prefix+= word[0]
                        word = word[1:]
            
                    if consonant == '':
                        word = word + 'yay'
                    else:
                        word += consonant_prefix + 'ay'
            
                    if is_upper:
                        word = word.upper()
                    elif is_title:
                        word = word.title()
                    pig_latin.append(prefix_non_alpha + word + suffix_non_alpha)
            
                pig_latin_text = "".join(pig_latin)
            
                print(pig_latin_text)


<a id="orgc3b49c5"></a>

### Implementation

I had to change two things, first the list for vowels it should include "y" and in the first loop to verify non-alpha characters I had to add the verification for the len of the string to be greater than 0. So the code end up like this:

    def main():
        text = input("Ingrese el texto a traducir: \n")
        text = text.split()
        pig_latin = []
    
        if not text:
            return
    
        for word in text:
            prefix_non_alpha = ''
            while len(word) > 0 and not word[0].isalpha() :
                prefix_non_alpha += word[0]
                word = word[1:]
            if len(word) == 0:
                pig_latin.append(prefix_non_alpha)
                continue
    
            suffix_non_alpha = ''
            while not word[-1].isalpha():
                suffix_non_alpha += word[-1]
                word = word[0:-1]
    
            is_upper = word.isupper()
            is_title = word.istitle()
    
            consonant_prefix= ''
            word = word.lower()
    
            while len(word) > 0 and not word[0] in "aeiouy":
                consonant_prefix+= word[0]
                word = word[1:]
    
            if consonant_prefix == '':
                word = word + 'yay'
            else:
                word = word + consonant_prefix + 'ay'
    
            if is_upper:
                word = word.upper()
            elif is_title:
                word = word.title()
            pig_latin.append(prefix_non_alpha + word + suffix_non_alpha)
    
        pig_latin_text = " ".join(pig_latin)
    
        print(pig_latin_text)

