---
layout: "language"
page_title: "Backend Overview - Configuration Language"
description: "A backend defines where Terraform stores its state. Learn about how backends work."
---

# Backends

Backends define where Terraform's [state](/docs/language/state/index.html) snapshots are stored.

A given Terraform configuration can either specify a backend,
[integrate with Terraform Cloud](/docs/language/settings/configuring-terraform-cloud),
or do neither and default to storing state locally.

The rest of this page introduces the concept of backends; the other pages in
this section document how to configure and use backends.

- [Backend Configuration](/docs/language/settings/backends/configuration.html) documents the form
  of a `backend` block, which selects and configures a backend for a
  Terraform configuration.
- This section also includes a page for each of Terraform's built-in backends,
  documenting its behavior and available settings. See the navigation sidebar
  for a complete list.

## What Backends Do

Backends primarily determine where Terraform stores its [state](/docs/language/state/index.html).
Terraform uses this persisted [state](/docs/language/state/index.html) data to keep track of the
resources it manages. Since it needs the state in order to know which real-world infrastructure
objects correspond to the resources in a configuration, everyone working with a given collection of
infrastructure resources must be able to access the same state data.

By default, Terraform implicitly uses a backend called
[`local`](/docs/language/settings/backends/local.html) to store state as a local file on disk.
Every other backend stores state in a remote service of some kind, which allows multiple people to
access it. Accessing state in a remote service generally requires some kind of access credentials,
since state data contains extremely sensitive information.

Some backends act like plain "remote disks" for state files; others support
_locking_ the state while operations are being performed, which helps prevent
conflicts and inconsistencies.

-> **Historical note:** Prior to Terraform 1.1.0, this documentation made a
distinction between "standard" and "enhanced" backends; we later decided that
wasn't useful. If you encounter old material that mentions "enhanced" backends,
it refers to the [remote](/docs/language/settings/backends/remote.html)
backend's ability to perform Terraform operations remotely in Terraform Cloud.
`remote` was the only "enhanced" backend, and
[the Terraform Cloud integration](/docs/language/settings/configuring-terraform-cloud)
is intended to replace it.

## Available Backends

Terraform includes a built-in selection of backends, which are listed in the
navigation sidebar. This selection has changed over time, but does not change
very often.

The built-in backends are the only backends. You cannot load additional backends
as plugins.

