# Translation examples

Recorded 2026-11-13. Verified with published CLI 5.70.2 and translation 1.10.3.

## Scope

These notes cover the boundary between the documentation source, CLI XLIFF extraction, and rendered examples. Public behavior is documented in `ru/tools/docs/translate.md` and its English counterpart.

## Entry points and verification

- CLI: `src/commands/translate/commands/extract.ts` passes no code mode to the translation library.
- Translation: `src/skeleton/rules/code/index.ts` chooses `all` when `compact` is false and no block mode is set. `src/skeleton/hooks/before-inline.ts` keeps inline code content as text between formatting tokens.
- CLI: `src/core/markdown/loader/resolve-no-translate.ts` handles build-time removal of exclusion directives.
- Check examples with `yfm translate extract --input ./fixtures --output ./xliff --source ru-RU --target en-US`, then `yfm translate compose --input ./xliff --output ./composed --use-source`.

## Behavior and pitfalls

- Exported code formatting is different from excluded content: inline code text is translatable even though its backticks become auxiliary tags. Protected inline content instead becomes an `x` tag with `equiv-text`.
- In the verified CLI version, `extract --code no` is accepted but does not change code extraction. Use per-block `translate=no` or exclusion directives in source examples.
- The build loader resolves no-translate directives before Markdown parsing, including inside code spans and fences. A successful build alone does not prove that documentation shows their literal syntax. Inspect the rendered code text. HTML `code`/`pre` with an encoded colon (`&#58;`) preserves the displayed syntax without changing what readers copy.
- Excess indentation can turn a fence into inline-like content. In the verified version, a fence indented seven spaces after `1. Run:` loses a newline on source composition, while the valid three-space version round-trips unchanged.

## Unverified areas

These checks do not verify external CAT tools, Azure DevOps rendering, or provider API responses. Recheck current releases before changing documented defaults.
