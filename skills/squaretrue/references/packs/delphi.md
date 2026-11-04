# Delphi pack

**Applies to:** Delphi / Object Pascal applications (VCL or FireMonkey), built with RAD Studio.

*Example pack: an illustration, not supported ecosystem coverage.*

## Detect

- `*.dpr`, `*.dpk`, `*.dproj`, or `*.groupproj` files.
- `*.pas` units with `*.dfm` (VCL) or `*.fmx` (FireMonkey) form files.

## Core obligations

### Manage resources safely

- Free every object you create unless an owner takes it: `Obj := TFoo.Create; try ... finally Obj.Free; end;`. Create the object **before** the `try`.
- Components with an `Owner` are freed by it. Freeing one earlier is also safe: its destructor removes it from the owner's list. Clear any other references to it (`FreeAndNil` on fields).
- Do not mix object references and interface references to the same reference-counted object; the reference count will free it under you.
- Use `FreeAndNil` for fields that are checked with `Assigned` later.

### Preserve concurrency safety

- Touch VCL/FMX controls only on the main thread. From a worker, use `TThread.Queue` (non-blocking) or `TThread.Synchronize`.
- Protect shared state with the project's existing mechanism (`TCriticalSection`, `TMonitor`, `TInterlocked`).
- Use a separate database connection per thread unless the driver documents otherwise.

### Access data safely

- Pass values through query parameters (`ParamByName(...).Value`), never by string concatenation into SQL.
- Wrap multi-statement writes in the connection's transaction (`StartTransaction` / `Commit` / `Rollback` in `try ... except`).
- Parse user input with explicit `TFormatSettings` where locale matters (decimal separator, dates).

### Verify changes

- Find the build in the `.dproj`/`.groupproj` and existing scripts; command-line builds run `msbuild` after `rsvars.bat` sets up the environment.
- Tests are usually DUnitX or DUnit projects in the group; run them in the console runner when present.
- Building the IDE-open project while the IDE holds unsaved buffers can test stale code; save or use the IDE's own build.

### Maintain UI consistency

- Reuse the project's styles (VCL Styles, FMX style books), frames, and base forms instead of setting colors and fonts per control.
- Keep `.dfm`/`.fmx` and `.pas` in sync: a component declared in one must exist in the other.

## Pitfalls

- **Exception in a constructor:** the destructor runs on a partially built object; destructors must tolerate `nil` fields.
- **`with` statements:** hide which object a name resolves to; do not add new ones.
- **Hand-editing `.dfm` / `.fmx`:** easy to corrupt; prefer the designer or keep edits minimal and re-open the form to check.
- **String types:** `string` is UTF-16; `AnsiString` and `PAnsiChar` calls into old APIs lose characters silently.
- **Leaks hidden at shutdown:** set `ReportMemoryLeaksOnShutdown := True` in debug builds to see them.
- **Freeing a component from its own event handler:** execution returns into freed memory. For a form, call `Release`; otherwise defer the free, for example with `TThread.ForceQueue`.
