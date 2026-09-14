# Cogito.Activities

Async and retry support for Windows Workflow Foundation, plus a set of activities that make WF
usable from ordinary C#.

## Why

WF predates `async`/`await`, so calling an async API from an activity means writing an
`AsyncCodeActivity` with `Begin`/`End` pairs by hand. Retry is likewise something every workflow
reinvents. This package provides both, and a fluent way to build activities from delegates instead of
constructing expression trees.

## Install

```shell
dotnet add package Cogito.Activities
```

## Awaiting inside an activity

```csharp
var activity = Expressions.Invoke(async () => await client.GetOrderAsync(id));
```

`AsyncTaskCodeActivity` is the base if you are writing your own. The task runs on an
`AsyncTaskExecutor`, so the workflow's scheduler is not blocked; `WithAsyncTaskExecutor` chooses
which executor a scope uses, and `ThreadPoolAsyncTaskExecutor` is the default.

## Retrying

```csharp
var activity = new Retry
{
    Body = DoTheWork(),
}
.WithAttempts(5)
.WithDelay(TimeSpan.FromSeconds(10));
```

`RetryCatch` narrows which exceptions are retried, and each caught attempt is emitted as a
`RetryExceptionCaughtTrackingRecord` so retries show up in tracking rather than disappearing.

## Driving a workflow

Extension methods give the `WorkflowApplication` API an async face — `RunAsync`, `LoadAsync`,
`UnloadAsync`, `PersistAsync`, `ResumeBookmarkAsync`, `WaitForCompletionAsync`.

`NoPersist` / `WithNoPersist` mark a region as non-persistable; `For`, `Branch`, `BranchWait`,
`AndAlso` and `FormatActivity` cover common shapes without hand-built expressions.

Targets .NET Framework — WF only exists there.

## License

MIT.
