# Mini-Shell 🐚

**42 School — Core Curriculum**

A small Unix shell implemented in C, built from scratch as part of the 42 School curriculum.

Mini-Shell recreates essential shell behavior: reading commands, parsing input, managing environment variables, executing programs, and working with pipes and redirections. The project explores how a shell interacts with the operating system through processes, file descriptors, and system calls.

This project was developed collaboratively by **Bushra Alhamadani** and **Raneem Abu-Salah**.

## Table of Contents

- [About](#about)
- [Features](#features)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)
- [Makefile Rules](#makefile-rules)
- [What We Learned](#what-we-learned)
- [Collaborators](#collaborators)

## About

A shell is a command-line interface that allows users to interact with an operating system by entering commands.

The goal of Mini-Shell is to implement a simplified shell in C while learning how command input is processed and executed. The project brings together several systems-programming concepts, including tokenization, parsing, environment handling, process creation, pipes, file redirection, and signal handling.

Rather than relying on an existing shell to execute the whole workflow, Mini-Shell implements its own command-processing and execution logic using Unix/POSIX system interfaces.

## Features

The mandatory implementation includes the core elements of a small interactive shell:

- **Interactive command prompt** — read and process commands entered by the user.
- **Tokenization and parsing** — break command input into meaningful tokens and parse it before execution.
- **Built-in commands** — implement shell commands that need to run within the shell process.
- **External commands** — launch executable programs.
- **Pipes (`|`)** — connect the output of one command to the input of another.
- **Input redirection (`<`)** — read command input from a file.
- **Output redirection (`>`)** — redirect command output to a file.
- **Append redirection (`>>`)** — append command output to a file.
- **Here-documents (`<<`)** — read input until a specified delimiter is encountered.
- **Environment variables** — access and manage environment values and expand variables in supported contexts.
- **Signal handling** — handle terminal signals during interactive use.
- **Exit status handling** — keep track of command execution status.

## How It Works

Mini-Shell processes a command through several stages:

1. **Read input** — receive a command from the interactive prompt.
2. **Tokenize** — identify words, quoted text, and shell operators.
3. **Parse** — organize the tokens into a structure that can be processed.
4. **Prepare execution** — resolve the command and prepare any required redirections or here-documents.
5. **Execute** — run built-in commands or create processes for external commands, setting up pipes and file descriptors when needed.
6. **Collect status and clean up** — wait for child processes, preserve the relevant exit status, and release resources before continuing.

This separation makes it easier to reason about how a command moves from raw text to an executed process.

## Project Structure

```text
Mini-Shell/
├── Makefile
├── libft/
│   └── libft.a                 # Built utility library
├── src/
│   ├── mini.c                  # Main shell entry point
│   ├── parcing/                # Tokenization and parsing
│   │   ├── node.c
│   │   ├── tokenizer1.c
│   │   ├── tokenizer2.c
│   │   ├── parsing1.c
│   │   ├── parsing2.c
│   │   └── parsing3.c
│   ├── execute/                # Command execution and redirections
│   │   ├── execute.c
│   │   ├── execute_child.c
│   │   ├── init_exec.c
│   │   ├── parent.c
│   │   ├── path.c
│   │   ├── prepforexecute.c
│   │   ├── redir.c
│   │   ├── redir2.c
│   │   ├── hd.c
│   │   ├── hd2.c
│   │   └── hd_expand.c
│   ├── built_in/                # Built-in commands
│   ├── utils/                   # Utility functions
│   └── signals.c                # Signal handling
└── README.md
```

The tree above highlights the main parts of the codebase. Some helper files are omitted for readability.

## Requirements

- Linux or another compatible Unix-like environment.
- A C compiler (`cc`).
- GNU Make.
- The GNU Readline development library.
- The included `libft` utility library, built through the Makefile.

On Debian or Ubuntu, install the common build tools and Readline development files with:

```bash
sudo apt update
sudo apt install build-essential libreadline-dev
```

## Installation

Clone the repository:

```bash
git clone https://github.com/balhamad/Mini-Shell.git
cd Mini-Shell
```

Compile the project from the repository root:

```bash
make
```

This builds the utility library and creates the `minishell` executable.

## Usage

Start Mini-Shell:

```bash
./minishell
```

Once the prompt appears, enter commands as you would in a regular shell.

To leave the shell, use the `exit` built-in or press `Ctrl+D` on an empty prompt.

## Examples

### Basic commands

```bash
minishell$ pwd
minishell$ echo "Hello, world!"
minishell$ ls -l
```

### Pipes

Pass the output of one command to another:

```bash
minishell$ ls | wc -l
minishell$ cat Makefile | grep minishell
```

### Redirections

Write command output to a file:

```bash
minishell$ echo "Hello from Mini-Shell" > output.txt
```

Append output to a file:

```bash
minishell$ echo "Another line" >> output.txt
```

Read command input from a file:

```bash
minishell$ cat < output.txt
```

### Environment variables

Use built-ins to inspect or change the shell environment:

```bash
minishell$ env
minishell$ export GREETING="Hello"
minishell$ echo "$GREETING"
minishell$ unset GREETING
```

### Here-documents

Provide input until a delimiter is entered:

```bash
minishell$ cat << EOF
> First line
> Second line
> EOF
```

These are example commands to try; exact behavior can differ from Bash, since Mini-Shell implements the project-required subset of shell behavior.

## Makefile Rules

Run these commands from the repository root:

| Command | Description |
|---|---|
| `make` | Build the library and Mini-Shell executable. |
| `make clean` | Remove generated object files and clean the library build. |
| `make fclean` | Remove object files, the executable, and generated library output. |
| `make re` | Perform a clean rebuild. |

## What We Learned

Working on Mini-Shell helped us develop a deeper understanding of how command-line interpreters work internally.

Key concepts explored in the project include:

- Tokenizing and parsing command input.
- Managing environment variables and shell state.
- Creating and waiting for processes.
- Connecting commands using pipes.
- Redirecting input and output with file descriptors.
- Handling here-documents and command execution.
- Responding to terminal signals.
- Managing memory and resources in a C program.
- Collaborating on a shared codebase and integrating different parts of a system.

## Collaborators

This project was developed as a collaboration between:

- **Bushra Alhamadani** — [@balhamad](https://github.com/balhamad)
- **Raneem Abu-Salah** — [@rabusalah](https://github.com/rabusalah)

Both collaborators contributed to the development of Mini-Shell as part of the 42 School curriculum.

---

*42 School — Core Curriculum*
