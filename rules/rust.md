# Rust code review checklist

When reviewing Rust code, audit against the following criteria:

## 1. Memory and allocations
- **Flag unnecessary cloning:** Look for `.clone()` and `.to_string()`. Challenge whether borrowed slices (`&str`, `&[T]`) or references (`&T`) could be used instead.
- **Audit stack vs. heap placement:** Question whether small, fixed-size data belongs on the heap. Ensure recursive data structures use appropriate heap indirection (`Box<T>`).
- **Inspect pointer representations:** Verify correct use of fat pointers (`&str`, `&[T]`) versus thin pointers. Check for accidental $O(n)$ character lookups versus $O(1)$ byte slices.

## 2. Ownership and mutation patterns
- **In-place mutations:** Flag functions that pass and return entire structs by value when a mutable reference (`&mut self`) is clearer and avoids moves across stack frames.
- **Disjoint borrowing:** When borrow conflicts arise, check if splitting borrows into local variables or accessing disjoint fields directly resolves the conflict.

## 3. Idiomatic design
- **Trait implementations:** Check whether custom comparison or printing logic should instead implement standard traits like `PartialEq`, `Eq`, or `Display`.
- **Exhaustive pattern matching:** Ensure match expressions handle error cases meaningfully rather than relying on uncontrolled panics.
