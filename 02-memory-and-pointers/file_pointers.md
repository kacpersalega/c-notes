# File Pointers

The abstraction of files that C provides is implemented in a data structure known as `FILE`

Some of the most common file I/O functions are:
- `fopen()`
- `fclose()`
- `fgetc()`
- `fputc()`
- `fread()`
- `fwrite()`

___

## fopen( )
- Opens a file and returns a file pointer to it.
- Always check the return value to make sure you don't get back `NULL`.

Syntax:

```c
FILE *ptr = fopen(<filename>, <operation>);
```
Example:
```c
FILE *ptr1 = fopen("file1.txt", "r");
```

Three options of opening a file are:
- `"r"` This lets you read the contents of a file
- `"w"` This lets you write to file, but opening in this mode erases all the contents of a file
- `"a"` This lets you to append to a file. Keeps previous content of a file untouched.

___

## fclose ( )
Quite self-explanatory. Closes the file pointed to by the given file pointer.

Syntax:

```c
fclose(<file pointer>);
```

Example:

```c
fclose(ptr1);
```
___

## fgetc ( )
- Reads and returns the next character from the file pointed to.
- The operation of the file pointer passed as in a parameter must be `"r"` for read or an error will occur.


Syntax:
```c
char ch = fgetc(<file pointer>);
```

Example:
```c
char ch = fgetc(ptr1);
```


Utilizing a `while` loop in combination with `fgetc()` basically allows us to replicate a `cat` command from linux:

```c
char ch;
while ((ch = fgetc(ptr)) != EOF)
    printf("%c", ch);
```
___

## fputc( )

- Writes or appends the specified character to the pointed-to file.
- The operation of the file pointer passed in as a parameter must be `"w"` for write or `"a"` for append, or and error will occur.

Syntax:
```c
fputc(<character>, <file pointer>);
```

Example:
```c
fputc('A', ptr1);
```

Now combining a `while` loop, `fputc()` and `fgetc()` we can essentially replicate linux `cp` command

```c
char ch;
while ((ch = fgetc(ptr)) != EOF)
    fputc(ch, ptr2);
```

___

## fread( )
- Reads `<qty>` units of `<size>` from the file pointed to and stores them in memory in a buffer (which is usually an array) pointed to by `<buffer>`
- The operation of the file pointer passed in as a parameter must be `"r"` for read, or an error will occur.

Syntax:
```c
fread(<buffer>, <size>, <qty>, <file pointer>);
```

<br>

Example 1:
```c
int arr[10];
fread(arr, sizeof(int), 10, ptr);
```
Here we are reading `10 * 4 bytes` of information from the file pointed to by ptr and we are storing them in an array `arr`.

<br>

Example 2:
```c
double *arr2 = malloc(sizeof(double) * 80);
fread(arr2, sizeof(double), 80, ptr);
```
In this example we are dynamically allocating memory (storing it on the heap.) We declare a `double *arr2` because malloc returns a pointer.

<br>

Example 3:
```c
char c;
fread(&c, sizeof(char), 1, ptr);
```
In this example we are treating `fread()` like a call to `fgetc()`. Note that we are using `&c` because the first argument in `fread()` is a pointer to the location in memory in which we want to store the information. 

In examples 1 & 2 we didn't have to write `&arr` or `&arr2` because the name of an array is a pointer :).

___

## fwrite( )
- Writes `<qty>` units of `<size>` to the file pointed to by reading them from a buffer (which is usually an array) pointed to by `<buffer>`
- The operation of the file pointer passed in as a parameter must be `"w"` for write or `"a"` for append, or and error will occur.

Syntax:
```c
fwrite(<buffer>, <size>, <qty>, <file pointer>);
```

<br>

Example 1:
```c
int arr[10];
// Some code between that fills arr
fwrite(arr, sizeof(int), 10, ptr);
```

<br>

Example 2:
```c
double *arr2 = malloc(sizeof(double) * 80);
fwrite(arr2, sizeof(double), 80, ptr);
```

<br>

Example 3:
```c
char c;
fwrite(&c, sizeof(char), 1, ptr);
```