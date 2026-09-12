# NWN Modbuild Template

Template repository for automatically building and publishing a
Neverwinter Nights: Enhanced Edition module via GitHub Actions.

On every push to `main` (or manually via `workflow_dispatch`), the module
is packed from the source files in `src/` using
[nasher](https://github.com/squattingmonk/nasher), zipped, and
automatically published as a GitHub Release.

## Usage

1. Create a new project from this repo via **"Use this template"**.
2. Update `nasher.cfg` (work through all `TODO` comments):
   - `name` / `description` of the package
   - `target.file` – name of the generated `.mod` file
3. Add/replace your module resources in `src/` (as JSON representations
   of the GFF files, e.g. `.ifo.json`, `.are.json`, `.itp.json`,
   `.fac.json`).
4. Push to `main` – the workflow builds the module and automatically
   creates a release containing the zipped `.mod` file.

## Workflow overview

`.github/workflows/create-release.yaml`:

1. Download/cache the official NWN server data (needed by nasher to
   compile scripts).
2. Install Nim + nasher (including `neverwinter.nim`/`nwn_script_comp`
   as the compiler).
3. `nasher pack --default` builds the `.mod` file.
4. The `.mod` file is zipped.
5. The zip is published as a GitHub Release (tag = build timestamp).

## Folder structure

```
src/          Module resources as JSON (nasher converts these to GFF/ERF)
nasher.cfg    Package/build configuration
```

## Requirements for local development

- [nasher](https://github.com/squattingmonk/nasher) installed locally,
  if you also want to build the module outside of CI.
