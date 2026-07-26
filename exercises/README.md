# Exercises

Every exercise moment in the 3-day schedule has several short, independent exercises (usually 3 to 5), instead of one single exercise. Each is a single markdown file: topics practiced, a short description, step-by-step instructions, and the full solution below it. Not everyone needs the same amount of time, working through more or fewer of them is exactly the point.

Exercises that touch a database table, a data area, a data queue, a service program, or the IFS need an actual IBM i to compile and run against, the others can be tried out in any RPGLE-capable editor with a connection to one.


## Day 1

**1.1** — after Free format basics
- [1.1.1. Hello world](<1.1.1. Hello world.md>)
- [1.1.2. Sending messages](<1.1.2. Sending messages.md>)
- [1.1.3. Compiling two ways](<1.1.3. Compiling two ways.md>)

**1.2** — after Control statements, Fields
- [1.2.1. Constants and control options](<1.2.1. Constants and control options.md>)
- [1.2.2. Field types](<1.2.2. Field types.md>)
- [1.2.3. Eval variants](<1.2.3. Eval variants.md>)

**1.3** — after Debugging
- [1.3.1. Step through with STRDBG](<1.3.1. Step through with STRDBG.md>)
- [1.3.2. Find the bugs](<1.3.2. Find the bugs.md>)
- [1.3.3. Debug a batch job](<1.3.3. Debug a batch job.md>)

**1.4** — after Selections and iteration, Arrays
- [1.4.1. If, elseif and select](<1.4.1. If, elseif and select.md>)
- [1.4.2. Loops](<1.4.2. Loops.md>)
- [1.4.3. Arrays and for-each](<1.4.3. Arrays and for-each.md>)
- [1.4.4. Sorting an array](<1.4.4. Sorting an array.md>)

**1.5** — after Data structures
- [1.5.1. Basic data structures](<1.5.1. Basic data structures.md>)
- [1.5.2. Template and likeds](<1.5.2. Template and likeds.md>)
- [1.5.3. Pos and overlay](<1.5.3. Pos and overlay.md>)
- [1.5.4. Data structures and arrays combined](<1.5.4. Data structures and arrays combined.md>)
- [1.5.5. Sorting arrays of data structures and PSDS](<1.5.5. Sorting arrays of data structures and PSDS.md>)


## Day 2

**2.1** — after Built-in functions, Subroutines
- [2.1.1. String built-in functions](<2.1.1. String built-in functions.md>)
- [2.1.2. Numeric and date built-in functions](<2.1.2. Numeric and date built-in functions.md>)
- [2.1.3. Array built-in functions](<2.1.3. Array built-in functions.md>)
- [2.1.4. Subroutines](<2.1.4. Subroutines.md>)

**2.2** — after Internal procedures
- [2.2.1. Basic procedures](<2.2.1. Basic procedures.md>)
- [2.2.2. Value, const and optional parameters](<2.2.2. Value, const and optional parameters.md>)
- [2.2.3. Passed and omitted](<2.2.3. Passed and omitted.md>)
- [2.2.4. Main procedure and on-exit](<2.2.4. Main procedure and on-exit.md>)

**2.3** — after Calling programs and API's, Error handling
- [2.3.1. Prototyping and calling a program](<2.3.1. Prototyping and calling a program.md>)
- [2.3.2. Executing a command with QCMDEXC](<2.3.2. Executing a command with QCMDEXC.md>)
- [2.3.3. Calling a C runtime API](<2.3.3. Calling a C runtime API.md>)
- [2.3.4. Error handling with monitor and on-error](<2.3.4. Error handling with monitor and on-error.md>)

**2.4** — after Native file access, DSPF/PRTF
- [2.4.1. Declaring a file and chain](<2.4.1. Declaring a file and chain.md>)
- [2.4.2. Setll, setgt and reade](<2.4.2. Setll, setgt and reade.md>)
- [2.4.3. Write, update and delete](<2.4.3. Write, update and delete.md>)
- [2.4.4. Printing with QPRINT](<2.4.4. Printing with QPRINT.md>)

**2.5** — after Embedded SQL
- [2.5.1. Singleton select and exists check](<2.5.1. Singleton select and exists check.md>)
- [2.5.2. A static cursor](<2.5.2. A static cursor.md>)
- [2.5.3. A dynamic cursor with block fetch](<2.5.3. A dynamic cursor with block fetch.md>)
- [2.5.4. Insert with an identity column](<2.5.4. Insert with an identity column.md>)


## Day 3

**3.1** — after External procedures (ILE concepts)
- [3.1.1. Modules and bind by copy](<3.1.1. Modules and bind by copy.md>)
- [3.1.2. A service program with binder language](<3.1.2. A service program with binder language.md>)
- [3.1.3. Calling a service program through a binding directory](<3.1.3. Calling a service program through a binding directory.md>)
- [3.1.4. Activation groups](<3.1.4. Activation groups.md>)

**3.2** — after Data areas, Data queues
- [3.2.1. Reading and writing a data area](<3.2.1. Reading and writing a data area.md>)
- [3.2.2. A sequence number generator with in-lock](<3.2.2. A sequence number generator with in-lock.md>)
- [3.2.3. Sending and receiving on a data queue](<3.2.3. Sending and receiving on a data queue.md>)

**3.3** — after Xml parsing, YAJL
- [3.3.1. Parsing XML with xml-into](<3.3.1. Parsing XML with xml-into.md>)
- [3.3.2. Generating JSON with YAJL](<3.3.2. Generating JSON with YAJL.md>)
- [3.3.3. Exporting JSON to the IFS](<3.3.3. Exporting JSON to the IFS.md>)
- [3.3.4. Parsing JSON with data-into and YAJLINTO](<3.3.4. Parsing JSON with data-into and YAJLINTO.md>)

**3.4** — after NoxDb
- [3.4.1. Parsing and reading with NoxDB](<3.4.1. Parsing and reading with NoxDB.md>)
- [3.4.2. Building and exporting a document with NoxDB](<3.4.2. Building and exporting a document with NoxDB.md>)
- [3.4.3. Arrays and iterating with NoxDB](<3.4.3. Arrays and iterating with NoxDB.md>)
- [3.4.4. Turning a query into a node tree](<3.4.4. Turning a query into a node tree.md>)
- [3.4.5. Guaranteed cleanup with monitor and on-exit](<3.4.5. Guaranteed cleanup with monitor and on-exit.md>)
