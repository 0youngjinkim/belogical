# Maintenance notes

## Section-number cross-references

SKILL.md and the modules in `skills/belogical/references/` cite each other by numbered section (e.g. `exec-summary.md §6`), matching the numbered headings (`## 6. ...`) in each module. These numbers are maintained by hand. When adding, removing, or reordering a section in any module:

1. Renumber that module's headings.
2. Update every reference to the shifted sections — search the repo for `§` to find them all (they live in SKILL.md and in other modules' headers and bodies).
