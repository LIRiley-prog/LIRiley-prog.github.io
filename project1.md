[Back to Portfolio](./)

Custom Map
==========

-   **Class:** CSCI 315 – Data Structure Analysis
-   **Grade:** In Progress
-   **Language(s):** C++
-   **Source Code Repository:** [CSCI-315-2026-Spring-Solutions-](https://github.com/LIRiley-prog/CSCI-315-2026-Spring-Solutions-)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The Custom Map project was built as part of CSCI 315 – Data Structure Analysis. The goal was to implement a Map data structure from scratch in C++ — similar to how `std::map` works in the C++ standard library, but built entirely by hand without using any built-in containers.

The Map stores key-value pairs and supports operations like inserting new entries, retrieving values by key, removing entries, and searching for keys using binary search. Internally, the data is kept in a sorted array, which makes lookup fast and predictable.

Building the Map also required implementing proper memory management — including a copy constructor and a copy assignment operator — to make sure the data structure behaves safely when copied or assigned to another variable.

## How to Compile and Run the Program

```bash
g++ -o map_test main.cpp Map.cpp
./map_test
```

## UI Design

The program runs as a command-line application. Test cases are run automatically on startup and print their results to the terminal. Output includes:

- **Inserted entries** — confirming key-value pairs were added successfully
- **Lookup results** — displaying values retrieved by key
- **Remove confirmations** — showing entries before and after deletion
- **Edge case results** — handling duplicate keys and out-of-range lookups

## Additional Considerations

This project reinforced core concepts in data structures including sorted storage, binary search, and manual memory management with `new` and `delete`. Implementing copy semantics (copy constructor and assignment operator) was a key challenge, requiring careful handling of dynamic memory to avoid double-frees and memory leaks.

[Back to Portfolio](./)
