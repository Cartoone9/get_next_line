<div align="center">
  <img src="https://i.ibb.co/cmF80PB/image.png" alt="Project score">
</div>

# get_next_line

This repository contains my get_next_line project, an assignment from the first circle of 42 School. The main goal was to build a function that could read text, line by line, from a given file. This project really helped solidify my understanding of how to handle files, the ins and outs of static variables, and smart ways to manage buffers in C using the stack.

## Table of Contents

- [About](#get_next_line)
- [Usage](#usage)
- [Example](#example)
- [Note on Project State](#note-on-project-state)
- [Known Issues & Fix Suggestions](#known-issues--fix-suggestions)
- [License](#license)
  
## Usage

This project is only asking for a function and not a working program, so you cannot compile it unless you add a main function like this one:

```C
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

#ifndef BUFFER_SIZE
# define BUFFER_SIZE 42
#endif

char *get_next_line(int fd);

int main(int argc, char **argv)
{
    int     fd;
    char    *line;
    int     line_count = 0;

    if (argc != 2)
    {
        fprintf(stderr, "Usage: %s <file_path>\n", argv[0]);
        return (1);
    }

    fd = open(argv[1], O_RDONLY);
    if (fd == -1)
    {
        perror("Error opening file");
        return (1);
    }

    printf("--- Testing get_next_line with file: %s ---\n", argv[1]);
    printf("BUFFER_SIZE: %d\n", BUFFER_SIZE);
    printf("---------------------------------------\n");

    while ((line = get_next_line(fd)) != NULL)
    {
        line_count++;
        printf("Line %d: %s", line_count, line);
        free(line);
    }

    if (close(fd) == -1)
    {
        perror("Error closing file");
        return (1);
    }

    printf("---------------------------------------\n");
    printf("Total lines read: %d\n", line_count);
    return (0);
}
```

The get_next_line function supports multiple file descriptors up to `FD_MAX` (defined as 512 in `get_next_line.h`) but this main function is only testing a single file at a time.

## Example
  
Using the main provided above:  
<img width="640" height="166" alt="image" src="https://github.com/user-attachments/assets/f03b0aef-8adb-453f-a40d-c840a34e34d2" />  
  
## Note on Project State

All projects from my 42 cursus are preserved in their state immediately following their final evaluation. While they may contain mistakes or stylistic errors, I've chosen not to alter them. This approach provides a clear and authentic timeline of my progress and learning journey as a programmer.

## Known Issues & Fix Suggestions

`ft_fill_stash()` in my get_next_line implementation contains an unprotected `malloc()` that could cause issues in edge cases.

## License

[MIT](https://choosealicense.com/licenses/mit/)
