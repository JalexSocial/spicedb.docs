---
title: "Getting Started"
description: "How to get started with SpiceDb."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "example-6a1a6be4373e933280d78ea53de6158e"
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

# SpiceDb Library Usage Guide for ASP.NET

This README provides instructions on how to incorporate the SpiceDb library into your ASP.NET projects. SpiceDb leverages .NET 8 capabilities to enhance your web application development process, particularly focusing on HTMX integration.

## Requirements

- **.NET Version**: .NET 8 or newer.

## Installation

SpiceDb is available as a NuGet package. You can install it using the .NET CLI with the following command:

```sh
dotnet add package SpiceDb
```

For the latest version and more details, visit the [SpiceDb NuGet package page](https://www.nuget.org/packages/SpiceDb).

## Configuration

After installing SpiceDb, you need to configure it in your `Program.cs` or startup configuration file. This setup involves specifying your application's root component, default layout, antiforgery strategy, and HTMX configurations. Here's how to add SpiceDb to your application builder:

```csharp
builder.AddSpiceDb(config =>
    {
        config.RootComponent = typeof(HtmxApp<AppLayout>);
        config.DefaultLayout = typeof(HtmxLayout<MainLayout>);
        config.AntiforgeryStrategy = AntiforgeryStrategy.GenerateTokensPerPage;
    })
    .WithHtmxConfiguration(config =>
    {
        config.SelfRequestsOnly = true;
    })
    .WithHtmxConfiguration("articles", config =>
    {
        config.SelfRequestsOnly = true;
        config.GlobalViewTransitions = true;
    });
```

### Configuration Details

- **RootComponent**: Defines the default root component for your component hierarchy. Wrapping a Layout in `HtmxApp` ensures that when a page is rendered with HTMX, it won't render the Layout.
- **DefaultLayout**: Applied to any view that doesn't specifically specify a Layout attribute.
- **AntiforgeryStrategy**: Configures antiforgery tokens behavior. Options include turning off antiforgery tokens, generating them on each request, or generating them on each full-page reload.

### HTMX Configuration

`WithHtmxConfiguration` allows setting up HTMX-specific settings, supporting both default and named configurations. In this example we configure:

- **SelfRequestsOnly**: Restricts HTMX requests to the same origin.
- **GlobalViewTransitions**: Enables global view transitions for the specified named configuration.

Multiple configurations can be defined for different parts of your application, offering granular control over HTMX behavior.

For more detailed information on configuring HTMX in SpiceDb, refer to the [Htmx Configuration Documentation](https://jalexsocial.github.io/SpiceDb.docs/docs/htmx/configuration/).

## Middleware

After configuring antiforgery and routing in your application, ensure to add the SpiceDb middleware to the pipeline:

```csharp
app.UseSpiceDb();
```

This middleware integrates SpiceDb's capabilities into your application, enabling advanced features and configurations specified in your setup.

## Conclusion

SpiceDb offers a powerful and flexible way to enhance your ASP.NET applications with advanced HTMX integration and configuration options. By following the setup instructions outlined above, you can leverage SpiceDb to create dynamic, interactive web applications using the latest .NET technologies.