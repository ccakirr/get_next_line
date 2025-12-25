# Get Next Line

A C function that reads text line-by-line from file descriptors with configurable buffer size and static memory management.

## Description

`get_next_line` is a function that reads and returns one line at a time from a file descriptor. It handles multiple file descriptors simultaneously using static variables and efficiently manages memory with a customizable buffer size.

## Features

- ✅ Reads one line at a time from any file descriptor
- ✅ Handles multiple file descriptors concurrently
- ✅ Configurable buffer size at compile time
- ✅ Efficient memory management with static variables
- ✅ Works with files, stdin, and network sockets
- ✅ Bonus: Multiple file descriptor support

## Function Prototype

```c
char *get_next_line(int fd);
```

### Parameters

- `fd`: File descriptor to read from

### Return Value

- Returns the line read from the file descriptor (including the newline character `\n` if present)
- Returns `NULL` when there's nothing left to read or an error occurs

## Compilation

### Standard Version

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c
```

### Bonus Version (Multiple FD Support)

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line_bonus.c get_next_line_utils_bonus.c
```

You can change `BUFFER_SIZE` to any positive value to adjust the reading buffer size.

## Usage Example

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd;
    char *line;

    fd = open("test.txt", O_RDONLY);
    if (fd == -1)
        return (1);

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }

    close(fd);
    return (0);
}
```

## File Structure

```
.
├── get_next_line.c              # Main function implementation
├── get_next_line.h              # Header file with prototypes
├── get_next_line_utils.c        # Helper functions
├── get_next_line_bonus.c        # Bonus: Multiple FD support
├── get_next_line_bonus.h        # Bonus header file
└── get_next_line_utils_bonus.c  # Bonus helper functions
```

## How It Works

1. **Reading**: The function reads from the file descriptor in chunks of `BUFFER_SIZE` bytes
2. **Buffering**: Data is stored in a static variable to persist between function calls
3. **Line Extraction**: When a newline character is found, the line is extracted and returned
4. **State Management**: Remaining data is kept in the static buffer for the next call

## Memory Management

- All returned lines must be freed by the caller
- The function handles internal memory allocation and deallocation
- Static variables are used to maintain state between calls
- Memory is properly freed on errors or end of file

## Technical Details

- Uses static variables for state persistence
- Handles edge cases (empty files, files without newlines, etc.)
- Supports reading from standard input (fd = 0)
- Compatible with multiple simultaneous file descriptors (bonus)
- Buffer size can be optimized based on use case

## Author

**ccakir** - [ccakirr](https://github.com/ccakirr)

## License

This project is part of the 42 curriculum and follows the school's guidelines.
