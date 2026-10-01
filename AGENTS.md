# NovaPoint guidance

NovaPoint is a SharePoint administration library and desktop solution. Start with [README](README.md), `src/NovaPoint.sln`, and the affected project file. The README still mentions .NET 6, but the inspected library and console tester target .NET 8; use current project files as the build contract.

The library's SharePoint, directory and authentication commands are under `src/NovaPointLibrary/Commands/`. Keep UI orchestration separate from those commands and preserve upstream license notices. Follow an operation through its parameters, authentication context and callers before changing behavior. Permission reports, tenant-wide enumeration, recycle-bin operations and copy/move commands have different scopes; do not treat all commands as read-only.

Use synthetic records for tests. Never commit tenant credentials, token caches, client secrets or report exports. Inspect authentication configuration without printing its values. A console tester is not a harmless unit-test suite: inspect its entry point and tenant targets before running it.

No automated CI or test runner was found in the inspected tree. Select a build command from the actual solution/project configuration on a compatible Windows/.NET environment; report the command and result rather than inventing an established gate. Build success alone does not prove live SharePoint behavior.

For tenant verification, obtain authorization for the exact tenant/site and operation, begin with read-only inspection, and use disposable data for mutations. Keep local source/build evidence separate from tenant readback. Document changes to permissions, identity handling or operation semantics in the nearby code and relevant `kb/` notes.
