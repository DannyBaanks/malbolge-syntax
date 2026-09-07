# malbolge-syntax — Gramatica TextMate para Malbolge

Gramatica TextMate con licencia MIT para [Malbolge](https://esolangs.org/wiki/Malbolge), publicada para `github-linguist/linguist`.

- **Alcance**: `source.malbolge`
- **Archivo**: `syntaxes/Malbolge.tmLanguage.json`
- **Version**: 0.1.0
- **Licencia**: MIT
- **Publicado**: `https://github.com/DannyBaanks/malbolge-syntax` en `4ec029d` (inicial) → fix de layout en `syntaxes/` (este commit)

## Alcance

`source.malbolge` reconoce caracteres ASCII imprimibles del fuente y marca los demas bytes que no son whitespace como invalidos. Intencionalmente **no** etiqueta caracteres individuales del fuente como instrucciones `i`, `o`, `*`, `p`, `/`, `<`, `v` o `j`.

En Malbolge, un caracter imprimible del fuente se normaliza con respecto a su posicion despues de quitar el whitespace. El opcode efectivo se calcula a partir de esa posicion, y el auto-cifrado posterior cambia la instruccion en tiempo de ejecucion otra vez. Las expresiones regulares de TextMate no mantienen el estado posicional mod-94 que se necesita. Resaltar un caracter como opcode basandose en su glyph seria una afirmacion semantica falsa. La gramatica resalta el fuente de forma uniforme en lugar de etiquetar bytes arbitrarios como instrucciones.

## Instalacion (VS Code)

Esta gramatica se consume via `github-linguist/linguist` (`grammars.yml` → `vendor/grammars/malbolge-syntax`). Para uso local en VS Code, copia `syntaxes/Malbolge.tmLanguage.json` y referencialo via `package.json` `contributes.grammars`.

## Validacion

- `syntaxes/Malbolge.tmLanguage.json` es JSON valido (`ruby -rjson` OK), `scopeName` `source.malbolge`, `fileTypes` `["malbolge"]`
- Seguro para PCRE, patrones lineales: `[^\\x09\\x0A\\x0D\\x20-\\x7E]` y `[!-~]`
- Ubicado en `syntaxes/` para que `grammar-compiler` de `github-linguist` lo descubra (`isValidGrammar` requiere `.../syntaxes/*.json` o `.../grammars/*.json`)
- El sample `tests/sample.malbolge` es el `truth_machine` (SHA `7062713e96dae33f5672fc4dcd654d5657e3c0ab44fd03bd93ebdd3ec43feb82`, 254 B)
- Probado via `script/add-grammar https://github.com/DannyBaanks/malbolge-syntax` desde un checkout limpio de `linguist` (ver `DannyBaanks/malbolge-linguist` `evidence/patches/malbolge.patch`)

## Upstream

Usado por `DannyBaanks/malbolge-linguist` `malbolge-patch` (`grammars.yml` `vendor/grammars/malbolge-syntax: - source.malbolge`, `languages.yml` `tm_scope: source.malbolge`).

## Licencia

MIT — ver `LICENSE`.
