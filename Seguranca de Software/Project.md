n4 - This vulnerability derives from the fact that we are appending "/" to resolved without taking into account if `resolved` has space for / and `wbuf`. This vulnerability is exploitable considering `wbuf` gets its value from copying it from `resolved`, and `resolved` gets its value from copying it from `path` which we have direct access considering it is given by the `args`. Therefore with the proper input we can write to space outside the buffer for `resolved` and therefore write outside the allocated stack frame.

```
Variaveis

*Confirmações com ifdef*

copiamos path para resolved com size MAXPATHLEN-1
colocamos \0 no MAXPATHLEN-1 de resolved

primero if
	remove os char ate ultimo /
	resolved = algo sem /
p = resolved
segundo if
	algo
	resolved  = ultimo valor diferent de \0
copiamos resolved para wbuf (wbuf tem size MAXPATHLEN por isso nao a problema)

*Confirmações com ifdef*

Se resolved for so / (estamos em root)
	root = 1
caso contrario
	root = 0

Se wbuf
	garantimos que len de wbuf + resolved + root + 1 > MAXPATHLEN
	se não estivermos na root
		append de / a resolved
	append de wbuf a resolved

```

5- This vulnerability can be easily solved by asserting the space allocated in resolved, and by making sure length of `resolved` >= to length of `wbuf` + 1.

6- This program is meant to scan data and sanitise it, it works by looping thorough the given input and making sure some characteristics are met, this being that all symbol are valid( not something we will exploit), and making sure some types of char have pairs to themselves, these being `()` and `<>` , the function makes sure that the string as these types of pairs by adding them if they are missing (we will exploit this).
This being said, the exploit is simple we will pass to the function a string missing one of these pairs and making sure that when the function adds this char to the string it leads to a buffer overflow. Considering it doesn't take into consideration it own added chars when calculating the length of the string.
```
main 
	adress with size char * 500 
	copy arg1 to adress
	delim = '\0'
	delimptr = NULL
	parseaddr

parseaddr
	pvpbuf with size PSBUFSIZE
	scan()

scan
	char *addr;
	int delim;
	char pvpbuf[];
	int pvpbsize;
	char **delimptr;
	u_char *toktab;
	q = pvpbuf
	do
		
	while
		tok = q
		infinite loop
			

```

7- A string like `<<<<<<<<<<<<<<<<<<<` could be used for this purpose (not sure)