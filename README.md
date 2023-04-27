<h1 align="center">
	<p>
		get_next_line
	</p>
</h1>
<h2 align="center">
	<p>
			A function that returns a line read from a file descriptor.
	</p>
</h2>
<p align="center">
Coded in
	<a href="https://skillicons.dev">
		<img src="https://skillicons.dev/icons?i=c" />
	</a>
</p>

## Table of Contents
- [The get_next_line function](#the-get_next_line-function)
- [Technical considerations](#Technical-considerations)
- [The functions](#The-functions)
- [The bonus part](#The-bonus-part)
- [Compilation](#Compilation)

### The get_next_line function

- Description:
  - The funtion takes a file descriptor "fd". Each time the function is called it returns one line from a file descriptor or NULL if the end of the file is reached.
  - Prototype:
  char	*get_next_line(int fd)
  - Return:
  The function either returns a NULL-terminated string which includes the newline (if end of file is not reached) or NULL if there is nothing left to read or an error occurred.

### Technical considerations
- Allowed external functions:
  - read()
  - malloc()
  - free()
- Norm:
  - Like my libft or ft_printf, this function has to be according to the norm of 42. Among others, this limits the amount of functions per file to five and the maximum lenght of a function to 25 lines. Since the subject only allows two .c files to be turned in, this limits it to 10 functions.
- BUFFER_SIZE:
  - The BUFFER_SIZE can be modified and the function still has to work, no matter if BUFFER_SIZE=1 or BUFFER_SIZE=10000.
- Memory:
  - To not use unnecessary memory, the static string should only contain what is not returned, this means the line has to be freed out of the buffer before being returned.
  - No memory leaks are tolerated, therefore all allocated memory has to be freed. This is especially tricky in this function, since the buffer is overwritten while freeing the returned line and while using the read function.

### The functions
- get_next_line()
  - Description: The main function, checks for wrong file descriptor or BUFFER_SIZE, calls the read_till(), set_line() and free_line() functions and returns the line.
  - Prototype: char	*get_next_line(int fd)
- read_till()
  - Description: Checks if there is a newline in the static string and reads, till either there is a newline in the string or the read function reads zero bytes (end of file). It calls strjoin() to add what was read to the end of the string.
  Prototype: char	*read_till(int fd, char *str)
- set_line()
  - Description: Gets the line from the static string and returns it as a null-terminated string.
  - Prototype: char	*set_line(char *str)
- free_line()
  - Description: Copies the string from the end of the line to the end into a temporary string and frees the string, it returns the temporary string. Since the string gets set to free_line() the returned value becomes the new value of the static string.
  - Prototype: char	*free_line(char	*str)
- ft_strjoin()
  - Description: It creates a new string by adding the second string passed to the back of the first one. The function was created in my [libft](https://github.com/itseugen/libft). For this it was modified to free the first string passed, since otherwise it couldn't be freed again and memory would leak.
  - Prototype: char	*ft_strjoin(char *s1, char *s2)
- ft_strlen()
  - Description: Returns the lenght of a string passed. The function is from my [libft](https://github.com/itseugen/libft).
  - Prototype: size_t	ft_strlen(const char *s)
- ft_strlcat()
  - Description: Adds the src to the end of dst as long as the dstsize has enough space. The function is from my [libft](https://github.com/itseugen/libft).
  - Prototype: size_t	ft_strlcat(char *dst, const char *src, size_t dstsize)
- ft_strchr()
  - Description: Returns a pointer to the first occurence of a character c in a string s, or NULL if c can't be found in the string. The function is from my [libft](https://github.com/itseugen/libft).
  - Prototype: char	*ft_strchr(const char *s, int c)

### The bonus part
- Requirements:
  In the bonus part, only one static variable was allowed and the get_next_line function must be able to read from multiple different file descriptors at once.
- Implementation:
  Since my normal get_next_line only needed one static variable to begin with, the first part of the bonus could be disregarded. To make the function able to read from multiple file descriptors at once, the static string was transformed into a 2D-Array. To account for more than enough file decriptors a size of 4096 was chosen.

### Compilation
- BUFFER_SIZE:
  As per requiremenents of the subject the buffer the read() function uses has to be a macro called BUFFER_SIZE. It is defined in the get_next_line.h. The predefined value of BUFFER_SIZE is 1024.
- Compiler Flags:
  It is possible to change the value of BUFFER_SIZE in the compiler call. To do this, the following flag gets added to the compiler call ``-D BUFFER_SIZE=n``. The n can be replaced by any value wished (if n <= 0 the function will always return NULL).

<sub><sup>This project is part of my studies at 42 Heilbronn</sup></sub>