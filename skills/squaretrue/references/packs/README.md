# Guidance packs

A guidance pack holds practices that are true for one ecosystem only. Squaretrue defines the format; teams write packs for their own stacks and link them from the `Squaretrue` section of their agent instruction file.

## Rules

- Load a pack only when the project uses its ecosystem (check its **Detect** section).
- Project-specific rules override a pack.
- A pack realizes the core obligations in [quality.md](../quality.md); it does not add workflow stages or grant permissions.
- The core workflow must stay useful without any pack.

## Format

Every pack is one Markdown file with these sections, in order:

| Section | Content |
|---|---|
| `# <Ecosystem> pack` | Title |
| `Applies to` | The ecosystem, in one line |
| `Detect` | Observable signals in a repository (files, manifests, dependencies) |
| `Core obligations` | One subsection per obligation in quality.md that has an ecosystem-specific realization; omit the ones that don't |
| `Pitfalls` | Known ecosystem traps, each with its fix |

Start from [_template.md](_template.md).

## Examples

These are illustrations, not supported ecosystem coverage:

- [delphi.md](delphi.md): native/desktop
- [typescript-react.md](typescript-react.md): web
