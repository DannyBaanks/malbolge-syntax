# Grammar Validation — Local

This package is **not published**. Validation is local only, pending explicit authorization to publish to `https://github.com/DannyBaanks/malbolge-syntax`.

## Checks performed (2026-09-02)

- `Malbolge.tmLanguage.json` is valid JSON (`ruby -rjson -e "JSON.parse(...)"` → OK)
- `scopeName` is `source.malbolge` (matches `languages.yml` candidate)
- `fileTypes` is `["malbolge"]` (primary extension `.malbolge`)
- Patterns are PCRE-safe, linear, no ReDoS: `[^\\x09\\x0A\\x0D\\x20-\\x7E]` and `[!-~]`
- `package.json` declares MIT, `contributes.grammars` points to `./Malbolge.tmLanguage.json`
- Sample `tests/sample.malbolge` is the truth_machine (SHA256 `7062713e96dae33f5672fc4dcd654d5657e3c0ab44fd03bd93ebdd3ec43feb82`), 254 B, single line

## Pending upstream validation

When authorized:
```bash
# from linguist checkout on branch malbolge-patch
script/add-grammar https://github.com/DannyBaanks/malbolge-syntax
# expected: registers vendor/grammars/malbolge-syntax, updates grammars.yml, caches license, sorts submodules
bundle exec rake samples # updates vendor/README.md
```

Until then `GRAMMAR_READY = FALSE` (technically `TRUE` locally, `BLOCKED` for PR). `TECHNICAL_IMPLEMENTATION_READY` will be `TRUE` once package is otherwise publish-ready.

See `README.md` for why the grammar does not try to label positional opcodes.
