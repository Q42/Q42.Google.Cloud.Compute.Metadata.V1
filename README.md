# GCE Metadata client

[![Tests](https://github.com/Q42/Q42.Google.Cloud.Compute.Metadata.V1/actions/workflows/verify-pr.yml/badge.svg)](https://github.com/Q42/Q42.Google.Cloud.Compute.Metadata.V1/actions/workflows/verify-pr.yml)
[![Publish](https://github.com/Q42/Q42.Google.Cloud.Compute.Metadata.V1/actions/workflows/publish-nuget.yml/badge.svg)](https://github.com/Q42/Q42.Google.Cloud.Compute.Metadata.V1/actions/workflows/publish-nuget.yml)

**Disclaimer: This is not an official Google package and has no affiliation with Google.**

This is a utility library for communicating with [Google Cloud metadata service](https://cloud.google.com/compute/docs/metadata/predefined-metadata-keys) on Google Cloud. Based on the [Go implementation](https://pkg.go.dev/cloud.google.com/go/compute/metadata#section-readme). Just like the Go implementation, this client will cache the responses from the metadata server.

## using the package

The best way to use the package is via dependency injection, since the package will cache the responses from the metadata api.

```csharp
builder.Services.AddSingleton<MetadataClient>();  
```

Alternatively you can also create a new client for a single call.

```csharp
  using var metadata = new MetadataClient();
  var onGce = await metadata.IsOnGCEAsync(context.CancellationToken);
```

### Errors when not running on GCE

By default the package does not throw any errors if you are not running on GCE and functions called will return null, however you can enable throwing errors by setting `throwIfNotOnGCE` to true when creating the client.

```csharp
using var metadata = new MetadataClient(throwIfNotOnGce: true);
```
