
# Development Journal

This is a journal the development process for this project. It is not intended to an extensive log of work, but rather a record of interesting challenges and errors and how they were resolved.

## Redirection/Piping

**Piping** is a way to connect the output of one program to the input of another program without any temporary file.

Commands

- `ls -l` lists the files in the current directory in long format.
- `wc -l` counts the number of lines in the input.

**Piping** connects the output of `ls -l` to the input of `wc -l`.

```bash
ls -l | wc -l
```

To save  the output of a command to a file (overwriting any existing content), use the `>` operator.

```bash
ls -l > file.txt
```

To append the output of a command to a file, use the `>>` operator.

```bash
ls -l >> file.txt
```

---
