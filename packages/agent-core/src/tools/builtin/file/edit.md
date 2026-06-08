Perform exact replacements in existing files.

- Edit is mandatory for every incremental change, especially small edits. Do not use Write or Bash `sed`.
- Take `old_string` and `new_string` from the Read output view.
- Drop the line-number prefix and tab; match only file content.
- `old_string` must be unique unless replace_all is set.
- If `old_string` is ambiguous, add surrounding context. Use replace_all only when every occurrence should change.
- Multiple independent Edit calls may run in one response.
- A write lock serializes same-file edits in response order.
- For dependent edits, order calls so each `old_string` still exists when executed; otherwise the call fails with `old_string not found`.
- For pure CRLF files, Read shows LF; use LF in `old_string` and `new_string`, and Edit writes CRLF back.
- For mixed endings or lone carriage returns, Read shows carriage returns as \r; include actual \r escapes in those positions.
