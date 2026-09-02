# Malbolge TextMate Grammar Candidate

This is a local MIT-licensed grammar candidate, deliberately outside the
Linguist checkout. It has not been published or added with
`script/add-grammar`; it is not an upstream dependency yet.

## Scope

`source.malbolge` recognizes printable ASCII source characters and marks other
non-whitespace bytes as invalid. It intentionally does not label individual
source characters as `i`, `o`, `*`, `p`, `/`, `<`, `v`, or `j` instructions.

In Malbolge, a printable source character is normalized relative to its position
after whitespace removal. The effective opcode is calculated from that
position, and later self-encryption changes the runtime instruction again.
TextMate regular expressions do not maintain the required modulo-94 positional
state. Highlighting a character as an opcode based on its glyph would therefore
make a false semantic claim. The grammar highlights valid source uniformly
instead of mislabeling arbitrary bytes as instructions.

## Upstream Path

1. Publish this grammar in an independent public repository.
2. Add validation fixtures that cover whitespace, invalid bytes, and positional
   source characters.
3. Run Linguist's `script/add-grammar <HTTPS URL>` from a clean checkout.
4. Only then add `tm_scope: source.malbolge` in Linguist.

Status: BLOCKED on publication and grammar-compiler validation.
