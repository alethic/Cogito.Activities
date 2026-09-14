# Cogito.Activities.ApplicationInsights

Sends Windows Workflow Foundation tracking records to Application Insights.

## Why

WF's tracking infrastructure can tell you exactly which activity ran, when, and why one faulted — but
only if something is listening. This is that listener, so workflow execution appears alongside the
rest of your telemetry instead of in a separate tracking store.

## Install

```shell
dotnet add package Cogito.Activities.ApplicationInsights
```

## Use

Add the participant to the workflow's extensions:

```csharp
var application = new WorkflowApplication(activity);
application.Extensions.Add(new ApplicationInsightsTrackingParticipant(telemetryClient));
```

Activity states, faults, and — when used with `Cogito.Activities` — caught retry attempts are
reported as Application Insights telemetry.

Targets .NET Framework.

## License

MIT.
