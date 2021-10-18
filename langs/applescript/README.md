## Apple Script

### Resources
- https://developer.apple.com/library/archive/documentation/AppleScript/Conceptual/AppleScriptLangGuide/conceptual/ASLR_fundamentals.html

### How to Run
``` bash
/usr/bin/osascript "filename.scpt"
```

### Basic Code Sample
``` AppleScript
property defaultClientName : "Mary Smith"

on greetClient(nameOfClient)

    display dialog ("Hello " & nameOfClient & "!")

end greetClient

script testGreet

    greetClient(defaultClientName)

end script

run testGreet --result: "Hello Mary Smith!"

greetClient("Joe Jones") --result: "Hello Joe Jones!"
```

### Comments
``` AppleScript
-- this is a comment
# this is also a comment
(* This
   Is
   A
   Multiline
   Comment *)
```
