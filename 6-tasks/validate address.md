
# validate address
```
import re

def validate_address(address):

    pattern = r'^\d+\s*,\s*st\s+[a-zA-Z\s]+[-][a-zA-Z]+$'
    
    return bool(re.match(pattern, address))

address = "22, st salah salem-Giza"

if validate_address(address):

    print("Valid address")
    
else:

    print("Invalid address")
 ```  

^: Start of the string.

\d+: Matches one or more digits (the house number).

\s*: Matches any whitespace (spaces or tabs).

,: Matches a comma.

\s*: Matches any whitespace.

st: Matches the literal string "st".

\s+: Matches one or more whitespace characters.

[a-zA-Z\s]+: Matches one or more alphabetic characters or spaces (for the street name).

[-]: Matches a hyphen.

[a-zA-Z]+: Matches one or more alphabetic characters (for the city or area).

$: End of the string.
