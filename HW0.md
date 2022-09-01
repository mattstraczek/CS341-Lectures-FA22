# Welcome to Homework 0!

For these questions you'll need the mini course and  "Linux-In-TheBrowser" virtual machine (yes it really does run in a web page using javascript) at -

http://cs-education.github.io/sys/

Let's take a look at some C code (with apologies to a well known song)-
```C
// An array to hold the following bytes. "q" will hold the address of where those bytes are.
// The [] mean set aside some space and copy these bytes into teh array array
char q[] = "Do you wanna build a C99 program?";

// This will be fun if our code has the word 'or' in later...
#define or "go debugging with gdb?"

// sizeof is not the same as strlen. You need to know how to use these correctly, including why you probably want strlen+1

static unsigned int i = sizeof(or) != strlen(or);

// Reading backwards, ptr is a pointer to a character. (It holds the address of the first byte of that string constant)
char* ptr = "lathe"; 

// Print something out
size_t come = fprintf(stdout,"%s door", ptr+2);

// Challenge: Why is the value of away equal to 1?
int away = ! (int) * "";


// Some system programming - ask for some virtual memory

int* shared = mmap(NULL, sizeof(int*), PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
munmap(shared,sizeof(int*));

// Now clone our process and run other programs
if(!fork()) { execlp("man","man","-3","ftell", (char*)0); perror("failed"); }
if(!fork()) { execlp("make","make", "snowman", (char*)0); execlp("make","make", (char*)0)); }

// Let's get out of it?
exit(0);
```

## So you want to master System Programming? And get a better grade than B?
```C
int main(int argc, char** argv) {
	puts("Great! We have plenty of useful resources for you, but it's up to you to");
	puts(" be an active learner and learn how to solve problems and debug code.");
	puts("Bring your near-completed answers the problems below");
	puts(" to the first lab to show that you've been working on this.");
	printf("A few \"don't knows\" or \"unsure\" is fine for lab 1.\n"); 
	puts("Warning: you and your peers will work hard in this class.");
	puts("This is not CS225; you will be pushed much harder to");
	puts(" work things out on your own.");
	fprintf(stdout,"This homework is a stepping stone to all future assignments.\n");
	char p[] = "So, you will want to clear up any confusions or misconceptions.\n";
	write(1, p, strlen(p) );
	char buffer[1024];
	sprintf(buffer,"For grading purposes, this homework 0 will be graded as part of your lab %d work.\n", 1);
	write(1, buffer, strlen(buffer));
	printf("Press Return to continue\n");
	read(0, buffer, sizeof(buffer));
	return 0;
}
```
## Watch the videos and write up your answers to the following questions

**Important!**

The virtual machine-in-your-browser and the videos you need for HW0 are here:

http://cs-education.github.io/sys/

The coursebook:

http://cs341.cs.illinois.edu/coursebook/index.html

Questions? Comments? Use Ed: (you'll need to accept the sign up link I sent you)
https://edstem.org/

The in-browser virtual machine runs entirely in Javascript and is fastest in Chrome. Note the VM and any code you write is reset when you reload the page, *so copy your code to a separate document.* The post-video challenges (e.g. Haiku poem) are not part of homework 0 but you learn the most by doing (rather than just passively watching) - so we suggest you have some fun with each end-of-video challenge.

HW0 questions are below. Copy your answers into a text document (which the course staff will grade later) because you'll need to submit them later in the course. More information will be in the first lab.

## Chapter 1

In which our intrepid hero battles standard out, standard error, file descriptors and writing to files.

### Hello, World! (system call style)
1. Write a program that uses `write()` to print out "Hi! My name is `<Your Name>`".
### Hello, Standard Error Stream!
2. Write a function to print out a triangle of height `n` to standard error.
   - Your function should have the signature `void write_triangle(int n)` and should use `write()`.
   - The triangle should look like this, for n = 3:
   ```C
   *
   **
   ***
   ```
### Writing to files
3. Take your program from "Hello, World!" modify it write to a file called `hello_world.txt`.
   - Make sure to to use correct flags and a correct mode for `open()` (`man 2 open` is your friend).
### Not everything is a system call
4. Take your program from "Writing to files" and replace `write()` with `printf()`.
   - Make sure to print to the file instead of standard out!
5. What are some differences between `write()` and `printf()`?

## Chapter 2

Sizing up C types and their limits, `int` and `char` arrays, and incrementing pointers

### Not all bytes are 8 bits?
1. How many bits are there in a byte?
2. How many bytes are there in a `char`?
3. How many bytes the following are on your machine?
   - `int`, `double`, `float`, `long`, and `long long`
### Follow the int pointer
4. On a machine with 8 byte integers:
```C
int main(){
    int data[8];
} 
```
If the address of data is `0x7fbd9d40`, then what is the address of `data+2`?

5. What is `data[3]` equivalent to in C?
   - Hint: what does C convert `data[3]` to before dereferencing the address?

### `sizeof` character arrays, incrementing pointers
  
Remember, the type of a string constant `"abc"` is an array.

6. Why does this segfault?
```C
char *ptr = "hello";
*ptr = 'J';
```
7. What does `sizeof("Hello\0World")` return?
8. What does `strlen("Hello\0World")` return?
9. Give an example of X such that `sizeof(X)` is 3.
10. Give an example of Y such that `sizeof(Y)` might be 4 or 8 depending on the machine.

## Chapter 3

Program arguments, environment variables, and working with character arrays (strings)

### Program arguments, `argc`, `argv`
1. What are two ways to find the length of `argv`?
2. What does `argv[0]` represent?
### Environment Variables
3. Where are the pointers to environment variables stored (on the stack, the heap, somewhere else)?
### String searching (strings are just char arrays)
4. On a machine where pointers are 8 bytes, and with the following code:
```C
char *ptr = "Hello";
char array[] = "Hello";
```
What are the values of `sizeof(ptr)` and `sizeof(array)`? Why?

### Lifetime of automatic variables

5. What data structure manages the lifetime of automatic variables?

## Chapter 4

Heap and stack memory, and working with structs

### Memory allocation using `malloc`, the heap, and time
1. If I want to use data after the lifetime of the function it was created in ends, where should I put it? How do I put it there?
2. What are the differences between heap and stack memory?
3. Are there other kinds of memory in a process?
4. Fill in the blank: "In a good C program, for every malloc, there is a ___".
### Heap allocation gotchas
5. What is one reason `malloc` can fail?
6. What are some differences between `time()` and `ctime()`?
7. What is wrong with this code snippet?
```C
free(ptr);
free(ptr);
```
8. What is wrong with this code snippet?
```C
free(ptr);
printf("%s\n", ptr);
```
9. How can one avoid the previous two mistakes? 
### `struct`, `typedef`s, and a linked list
10. Create a `struct` that represents a `Person`. Then make a `typedef`, so that `struct Person` can be replaced with a single word. A person should contain the following information: their name (a string), their age (an integer), and a list of their friends (stored as a pointer to an array of pointers to `Person`s).
11. Now, make two persons on the heap, "Agent Smith" and "Sonny Moore", who are 128 and 256 years old respectively and are friends with each other.
### Duplicating strings, memory allocation and deallocation of structures
Create functions to create and destroy a Person (Person's and their names should live on the heap).
12. `create()` should take a name and age. The name should be copied onto the heap. Use malloc to reserve sufficient memory for everyone having up to ten friends. Be sure initialize all fields (why?).
13. `destroy()` should free up not only the memory of the person struct, but also free all of its attributes that are stored on the heap. Destroying one person should not destroy any others.

## Chapter 5 

Text input and output and parsing using `getchar`, `gets`, and `getline`.

### Reading characters, trouble with gets
1. What functions can be used for getting characters from `stdin` and writing them to `stdout`?
2. Name one issue with `gets()`.
### Introducing `sscanf` and friends
3. Write code that parses the string "Hello 5 World" and initializes 3 variables to "Hello", 5, and "World".
### `getline` is useful
4. What does one need to define before including `getline()`?
5. Write a C program to print out the content of a file line-by-line using `getline()`.

## C Development

These are general tips for compiling and developing using a compiler and git. Some web searches will be useful here

1. What compiler flag is used to generate a debug build?
2. You modify the Makefile to generate debug builds and type `make` again. Explain why this is insufficient to generate a new build.
3. Are tabs or spaces used to indent the commands after the rule in a Makefile?
4. What does `git commit` do? What's a `sha` in the context of git?
5. What does `git log` show you?
6. What does `git status` tell you and how would the contents of `.gitignore` change its output?
7. What does `git push` do? Why is it not just sufficient to commit with `git commit -m 'fixed all bugs' `?
8. What does a non-fast-forward error `git push` reject mean? What is the most common way of dealing with this?

## Optional (Just for fun)
- Convert your a song lyrics into System Programming and C code and share on Ed.
- Find, in your opinion, the best and worst C code on the web and post the link to Ed.
- Write a short C program with a deliberate subtle C bug and post it on Ed to see if others can spot your bug.
- Do you have any cool/disastrous system programming bugs you've heard about? Feel free to share with your peers and the course staff on Ed.

************************HW 0 ANSWERS*****************************

Chapter 1:
1: #include <stdio.h>

int main() {
	write(1, "Hi! My name is Matt", 19);
	return 0;
}

2: #include <stdio.h>

void write_triangle(int n);

int main() {
	write_triangle(3);
	return 0;
}

void write_triangle(int n) {
	int i;
	for(i = 1; i < n + 1; i++) {
		int j;
		for (j = 0; j < i; j++) {
			write(1, "*", 1);
		}
		write(1, "\n", 1);
	}
}

3: #include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>


int main() {
	mode_t mode = S_IRUSR | S_IWUSR;
	int filedes = open("hello_world.txt", O_CREAT | O_TRUNC | O_RDWR, mode);
	write(filedes, "Hi! My name is Matt", 19);
	close(filedes);
	return 0;
}

4: 
int main() {
	mode_t mode = S_IRUSR | S_IWUSR;
	int filedes = open("hello_world.txt", O_CREAT | O_TRUNC | O_RDWR, mode);
	dprintf(filedes, "Hi! My name is Matt", 19);
	close(filedes);
	return 0;
}

5: write is lowlevel, printf can print integers

Chapter 2:
1: There are atleast 8 bits in a byte
2: There is 1 byte in a char
3: int: 4, double: 8, float: 4, long: 4, long long: 8
4: 0x7fbd9d50
5: data[3] == data + 3
6: Strings in C that are initialized in this way have their memory address noted as “read only,” so trying to write to that memory address produces a segmentation fault.
7: 12
8: 5
9: X = “ab”
10: Y = 1

Chapter 3:
1: One way is to check the value of argc. Another way is to loop through every arg element in argv until reaching the end of the arguments, or null.
2: argv[0] represents the first command, or the running of the exec file
3: On top of the stack
4: If the machine is 32 bit, sizeof(ptr) = 4, and if the machine is 64 bit, sizeof(ptr) = 8; sizeof(array) = 6. This is due to the ptr needing 4 bytes of storage to hold the value for its memory address, and array needing 6 bytes of storage, using one byte for each char (including \0).
5: A stack data structure manages the lifetime of automatic variables.

Chapter 4:
1: If you want to use data after the lifetime of the function that it was used in ends, you can store that data on the heap, keeping track of it with a pointer. This heap allocation can be done with the malloc() function, which takes in a size in bytes parameter to determine the desired size of allocation.
2: Stack memory is allocated for function calls and local variables, whereas the heap can store malloc’d variables that exist beyond the lifetimes of functions, but such variables must have their memory eventually free’d.
3: Static
4: In a good C program, for every malloc, there is a free.
5: If the program has used up all of the heap memory, malloc can fail.
6: time returns a time_t type, whereas ctime returns a more readable string representation of this time_t type. Another difference includes the fact that ctime returns static data, which means upon every time it is called, previous pointers have their respective data overwritten, whereas time does not have this attribute.
7: Attempting to free the same space of memory twice can confuse the program, since that area of memory may be used by the program to note whether it is actually free or not after the first free, in a way “bookkeeping.”
8: Since the memory for ptr has already been free’d, the respective data used in the printf function is no longer valid to be used.
9: One can avoid these previous two mistakes by programming without “dangling pointers,” or pointers that point to invalid memory. This can be accomplished by setting a respective pointer to NULL immediately after it is free’d.
10: 
typedef struct Person person_t;
struct Person {
	char* name;
	int age;
	person_t* friends[20];
};
11:
person_t* agent_smith = (person_t*) malloc(sizeof(person_t));
person_t* sonny_moore = (person_t*) malloc(sizeof(person_t));
	
agent_smith->age = 128;
sonny_moore->age = 256;

agent_smith->name = “Agent Smith”;
sonny_moore->name = “Sonny Moore”;
	
agent_smith->friends[0] = sonny_moore;
sonny_moore->friends[0] = agent_smith;;
	
free(agent_smith);
free(sonny_moore);

12:
person_t* create(char* name, int age) {
	person_t* person = (person_t*) malloc(sizeof(person_t));
	person->age = age;
	person->name = strdup(name);
	for (int i = 0; i < 20; i++) {
		person->friends[i] = NULL;
	}
	return person;

13: 
void destroy(person_t* person) {
	free(person);
}
Chapter 5:
1: getchar(), putchar()
2: gets() can accept input that is too long for the memory that it is responsible for, consequently overwriting other data.
3: 
char* data = “Hello 5 World”;
char first_str[20];
int first_int;
char second_str[20];
sscanf(data, “%s %d %s”, first_str, &first_int, second_str);
printf("%s %d %s", first_str, first_int, second_str);
4: Define _GNU_SOURCE
5: 
char* buffer = NULL;
size_t capacity = 0;
ssize_t result = getline( &buffer, &capacity, stdin);
if (result > 0 && buffer[result-1] == ‘\n’) {
	Buffer[result-1] = 0;
}
printf(“%d : %s\n”, result, buffer);
free(buffer);

C Development

1: -g flag
2: You must mark all objects up to date with make -t.
3: tabs
4: “git commit” essentially saves the current staged changes.SHA stands for Simple Hashing Algorithm, where all the changes in the commit are combined to generate a 40 character string as a sort of “identity” for the committed changes.
5: git log shows a list of all commits made to a repository
6: git status shows you which commits have or haven’t been staged. It doesn’t show you which files are being ignored however, which can be modified in the .gitignore file.
7: git push updates your project’s repository by “pushing” all of the committed changes to it. A commit message like this is insufficient because it is very ambiguous, and can lead to a lot of confusion later on in development.
8: This error means that git is unable to commit your changes. The most common ways of dealing with this is to either git pull to make sure your version is up to date, or to verify that you are committing to the correct project.


