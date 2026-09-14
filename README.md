# Cogito.Activities

[![Build](https://github.com/alethic/Cogito.Activities/actions/workflows/Cogito.Activities.yml/badge.svg)](https://github.com/alethic/Cogito.Activities/actions/workflows/Cogito.Activities.yml)

Async and retry support for Windows Workflow Foundation, so WF activities can await ordinary .NET APIs and recover from transient failures.

## Packages

**[Cogito.Activities](https://www.nuget.org/packages/Cogito.Activities)** — Async and retry support for Windows Workflow Foundation, plus a set of activities that make WF usable from ordinary C#.

**[Cogito.Activities.ApplicationInsights](https://www.nuget.org/packages/Cogito.Activities.ApplicationInsights)** — Sends Windows Workflow Foundation tracking records to Application Insights.

Each package carries its own README with the detail; the links above go to nuget.org.

## Building

```shell
dotnet restore Cogito.Activities.slnx
dotnet msbuild -p:Configuration=Release Cogito.Activities.dist.msbuildproj
```

Packages are staged into `dist/nuget` and test suites into `dist/tests`; run a suite with
`dotnet test -f <tfm> <path to its assembly>`.

## License

MIT — see [LICENSE](LICENSE).
