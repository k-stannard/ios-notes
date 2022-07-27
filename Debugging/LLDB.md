# Debugging with LLDB

## lldb console commands

po *variable* - console will print out the value of said variable

expression *variable* = *value* - xcode will set the specified value for said variable and evaluate it. 

## editing breakpoints & persisting values for debugging

You can edit breakpoints & specify a certain value so you don't have to keep setting an `expression` value every time you run your code.
> Right click, edit breakpoint  
> add action to the breakpoint  
> set the expression you want to use  
> check the option to automatically continue after evaluating an action  

