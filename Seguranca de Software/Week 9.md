
Exercise 1

1)
./date --date='TZ="America"234" 00:00 next Fri' or ./date --date='TZ="123"234" 00:00 next Fri'

will be valid inputs to crash the function

2)

The following command will allow us to use one of the crash cases to crash the date function 
./src/date -f outDir/crashes/id\:000001\,sig\:11\,src\:000206\,op\:flip1\,pos\:12 

(assuming we are in coreutils)

3)

In gdb we can see that the problem comes from main -> batch_convert -> parse_datetime and that it leaves date.c after that leading to the file parse_datetime.y

4)

By using gdb to analyse the error we concluded that even though the errors are said to be unique, all of them stem from the same line of code being the line that eventualy leads to parse_datetime



Exercise 2