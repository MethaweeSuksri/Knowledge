---
status: done
Recall: None
source: trust me bro
---

#process

---

# What pipe is

A pipe `|` is a shell operator that connects the **stdout of one command to the stdin of the next command**.

```text
command1 stdout ──→ pipe ──→ command2 stdin
```

>[!tip]
>
> To revise what stdout/in/err is. See [[standard stream]] 
## How pipe works

The shell starts both programs and establishes a connection between them.

The pipe is a **live stream between processes**, not a temporary file (important) containing the first command's completed output.

- The first program writes data to its **stdout**.
    
- That data enters the pipe.
    
- The second program can read that data from its **stdin**.
    
- Both programs can run at the same time.
    
- If the pipe's buffer fills up, the writing program waits until the reader consumes some data.
    
- If the reader has no data yet, it can wait until the writer produces some.

The receiving program decides whether and when to read from stdin.

### What if one program finishes first?

The programs do **not** need to finish at the same time.

If **A finishes first**, it closes its writing end of the pipe. B can continue reading any remaining buffered data. Once all data has been consumed, B receives **EOF**, meaning there will be no more input.

If **B finishes first**, the reading end of the pipe is closed. If A later tries to write to the pipe, the operating system notifies A that there is no reader, normally through **SIGPIPE**.

This is intentional behavior, not a failure of the pipe. A pipe is a **streaming connection**, not a guarantee that the producer must finish before the consumer can finish.

> [!clarification]
> 
> **Question**: Is a command's argument and stdin the same thing?
> 
> **Previous belief**:  
> I thought "input to a command" was one thing, and that the pipe somehow passed the output of one command as the input/argument of the next command.
> 
> **Correction**:  
> They are **two different input mechanisms**. When a program starts, it can receive:
> 
> 1. **Command-line arguments (`argv`)**
>     
> 2. **Standard input (`stdin`)**
>     
> 
> **Why confusing**:  
> Both can be thought of as "input", but they enter the program through completely different mechanisms. Arguments are given to the program when it starts; stdin is a stream that the program can read while it runs.
> 
> **Distinction**:
> 
> ```text
>             program
>            /       \
>       arguments    stdin
>        (argv)       (fd 0)
>          │             │
>          │             │
>       given when    stream of
>       program starts  bytes
> ```
> 
> A pipe connects **streams**, not arguments:
> 
> ```text
> A stdout ──→ pipe ──→ B stdin
> ```
> 
> It does **not** convert the output of A into command-line arguments for B.

