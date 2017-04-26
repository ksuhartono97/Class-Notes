# File System

File is always a contiguous logical address space.

Typical File Attributes:

- Name
- Identifier
- Type
- Location
- Size
- Protection
- Time, date, and user identification

## Open Files

Open file table: tracks open files, system-wide (all the files open in the system) and per-process (all the files open in the process).

## Acyclic-Graph directories

Natural extension from tree directory. Allows sharing of a directory.

Has a problem, the shared files no longer have a unique pathname. This results in the possibility of having an **alias**. But this creates the issue of clearing up the reference to the file on deletion. Because now there are 2 paths, if we delete one of them, but forgot to delete the other one, the other one will be a dangling pointer that points to empty/wrong files.

Yet if there is a cycle it can be very bad for the filesystem.

## File sharing

Divides users into three categories:

- Owners
- Groups
- General Public

The owner can then control access rights.

In UNIX, the owner can very easily change these access rights, there are 3 things that can be changed:

- R : Read
- W : Write
- X : Execute

The owner can then control these 3 bits, for each user group, giving specific groups certain permissions.

In UNIX, you can use the command `chmod` to modify these permissions.
