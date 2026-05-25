# Tamp.CycloneDx.V6

> Tamp CommandPlan wrapper for the `dotnet-CycloneDX` global tool (6.x) — generates CycloneDX SBOMs from .NET projects and solutions. Defaults to JSON output because the Tamp security chain (Dependency-Track / DefectDojo) consumes JSON.

| Package | Status |
|---|---|
| `Tamp.CycloneDx.V6` | 1.11.2 (post-migration from main `tamp`) |

## Install

```bash
dotnet add package Tamp.CycloneDx.V6
```

Multi-targets net8 / net9 / net10. Requires `dotnet-CycloneDX` 6.x installed (e.g. `dotnet tool install -g CycloneDX --version "6.*"`).

## Quick start

```csharp
using Tamp;
using Tamp.CycloneDx.V6;

class Build : TampBuild
{
    public static int Main(string[] args) => Execute<Build>(args);

    [Solution] readonly Solution Solution = null!;
    [FromPath("dotnet-CycloneDX")] readonly Tool CycloneDxBin = null!;

    Target Sbom => _ => _.Executes(() => CycloneDx.Generate(CycloneDxBin, s => s
        .SetProject(Solution.Path)
        .SetOutputDirectory(RootDirectory / "artifacts" / "security")
        .SetFilename("sbom.cyclonedx.json")
        .SetFormat(CycloneDxFormat.Json)
        .SetSpecVersion("1.6")));
}
```

## Verb surface (v1)

| Verb | Wraps | Required |
|---|---|---|
| `Generate` | `dotnet-CycloneDX <project> -o <dir> -fn <file> -of <format>` | Project path + output directory |

## Why 6.x

The 5→6 boundary in `dotnet-CycloneDX` was breaking enough to warrant a pinned wrapper:

- `--json` renamed to `--output-format Json`
- `--include-xml` / `--exclude-transitive` / `--set-serial-number` removed
- Default spec version shifted from 1.4 to 1.7

When CycloneDX 7 ships, this wrapper stays at 6.x and a sibling `Tamp.CycloneDx.V7` will track the new major.

## Why a satellite repo

This package previously shipped from the main `tamp` repo (1.11.0 / 1.11.1). It moved to its own satellite at 1.11.2 (TAM-254 / TAM-259) so that:

- CycloneDX tool releases don't gate Tamp.Core releases (and vice versa)
- Adopters can pin the wrapper independently of Tamp.Core minors
- The wrapper's release cadence tracks `dotnet-CycloneDX` instead of the whole framework

Package ID and version line are unchanged — adopters see no break.

## License

MIT — see [LICENSE](LICENSE).
