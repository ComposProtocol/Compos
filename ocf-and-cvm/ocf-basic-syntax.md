# OCF Basic Syntax

The basic syntax of the `func` part in OCF uses the Rust programming language(**version 1.76.0**). Rust is a powerful language, **but we have temporarily restricted some of its advanced syntax elements** to ensure swift and secure experimentation.

Currently, we have imposed the following limitations on OCF:

* OCF `func` is stateless and does not support deployers' custom variable definitions. Although the CVM has a system state, OCF deployers cannot define new states.
* OCF `func` can only contain one statement, supporting the use of system functions and operators to form this statement.
* OCF `func` doesn't support loops, structs, enums, pattern matching, Crates, collections, error handling, traits, closures, etc.

**The above restrictions will gradually be relaxed to unleash Rust's full potential**.

Developers' `func` code is deployed in the CVM, a WASM-based virtual machine implemented by Compos Protocol. We plan to open-source the entire project soon.
