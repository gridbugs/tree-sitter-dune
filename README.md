# tree-sitter-dune

[![CI](https://github.com/emillon/tree-sitter-dune/workflows/CI/badge.svg)](https://github.com/emillon/tree-sitter-dune/actions)

Tree-sitter grammar for [Dune](https://dune.readthedocs.io/) build system files.

## Features

- **Complete dune file support**: Parses all major stanzas including `executable`, `library`, `rule`, `test`, `alias`, and more
- **dune-project support**: Support for project metadata files including `lang`, `name`, `version`, `package`, and all project configuration stanzas
- **dune-workspace support**: Support for workspace configuration including `context`, `profile`, and cross-compilation setup
- **Syntax highlighting**: Highlight queries for editor integration
- **Field markers**: Structured AST with named fields for precise code navigation

## Supported File Types

- `dune` - Build files in each directory
- `dune-project` - Project metadata and configuration
- `dune-workspace` - Workspace-level settings and build contexts

## Installation

Nothing published to package repositories just yet, it's still in development.

## Usage

### With tree-sitter CLI

```bash
tree-sitter parse example.opam
```

## Grammar Coverage

### dune files

✅ **Fully Supported:**
- `executable`, `executables` - Build executables
- `library` - OCaml libraries
- `test`, `tests` - Test executables
- `rule` - Custom build rules with actions
- `alias` - Named build targets
- `install` - Installation rules
- `toplevel` - Custom toplevels
- `copy_files` - File copying with globs
- `include` - Include dune fragments
- `menhir` - Menhir parser generator
- `ocamllex`, `ocamlyacc` - Lexer/parser generation
- `foreign_library` - C/C++ libraries
- `plugin` - Compiler plugins
- `mdx` - Markdown executable blocks
- `coq.theory` - Coq integration
- `cram` - Cram tests
- `subdir` - Nested directories
- `env` - Environment configuration
- `ignored_subdirs` - Ignore directories
- `deprecated_library_name` - Library renaming
- Actions: `run`, `bash`, `copy`, `diff`, `write-file`, `with-stdout-to`, `progn`, and 15+ more

### dune-project files

✅ **Fully Supported:**
- `lang` - Language version (required)
- `name`, `version`, `license` - Project metadata
- `authors`, `maintainers`, `maintenance_intent` - Contributors
- `homepage`, `documentation`, `bug_reports` - URLs
- `source` - Repository information (github/git/uri)
- `package` - Package definitions with complex dependencies
- `generate_opam_files`, `opam_file_location` - OPAM integration
- `using` - Extension configuration (menhir, coq, etc.)
- `formatting` - Formatter settings
- `dialect` - Custom dialects
- `pin` - Pin dependencies
- `warnings` - Compiler warnings config
- `explicit_js_mode` - JavaScript mode
- `subst` - Watermarking
- Boolean flags: `accept_alternative_dune_file_name`, `executables_implicit_empty_intf`, `expand_aliases_in_sandbox`, `implicit_transitive_deps`, `map_workspace_root`, `use_standard_c_and_cxx_flags`, `wrapped_executables`

### dune-workspace files

✅ **Fully Supported:**
- `context` - Build contexts
  - `(context default)` - Default context
  - `(context (opam ...))` - Opam switch contexts
  - Fields: `switch`, `name`, `profile`, `toolchain`, `host`, `target`
  - Flags: `merlin`, `generate_merlin_rules`, `disable_dynamically_linked_foreign_archives`
  - Additional: `root`, `lock_dir`, `paths`, `env`, `fdo`, `targets`
- `profile` - Build profile selection (dev/release/custom)


## Contributing

Contributions are welcome! Please:

1. Add tests for any new features in `test/corpus/`
2. Ensure all tests pass with `tree-sitter test`
3. Update this README if adding new stanza support
4. Follow the existing code style

### Adding New Stanzas

1. Define the stanza in `grammar.js`:
   ```javascript
   _stanza_my_new_stanza: ($) =>
     dune_stanza(
       $,
       "my_stanza",
       choice(
         dune_field($, "field_name", $.value_type),
         $.sexp,
       ),
     ),
   ```

2. Add it to the `stanza` choice list
3. Create tests in `test/corpus/`
4. Run `tree-sitter generate && tree-sitter test`

## Resources

- [Dune Documentation](https://dune.readthedocs.io/)
- [Tree-sitter Documentation](https://tree-sitter.github.io/)
- [Grammar Development Guide](https://tree-sitter.github.io/tree-sitter/creating-parsers)

## License

MIT
