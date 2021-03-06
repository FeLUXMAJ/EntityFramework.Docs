---
title: Log of provider-impacting changes - EF Core
author: ajcvickers
ms.author: avickers
ms.date: 08/08/2018
ms.assetid: 7CEF496E-A5B0-4F5F-B68E-529609B23EF9
ms.technology: entity-framework-core
uid: core/providers/provider-log
---

# Provider-impacting changes

This page contains links to pull requests made on the EF Core repo that may require authors of other database providers to react. The intention is to provide a starting point for authors of existing third-party database providers when updating their provider to a new version.

We are starting this log with changes from 2.1 to 2.2. Prior to 2.1 we used the [`providers-beware`](https://github.com/aspnet/EntityFrameworkCore/labels/providers-beware) and [`providers-fyi`](https://github.com/aspnet/EntityFrameworkCore/labels/providers-fyi) labels on our issues and pull requests.

### 2.1 ---> 2.2

#### Test-only changes

* https://github.com/aspnet/EntityFrameworkCore/pull/12057 - Allow customizable SQL delimeters in tests
  * Test changes that allow non-strict floating point comparisons in BuiltInDataTypesTestBase
  * Test changes that allow query tests to be re-used with different SQL delimeters
* https://github.com/aspnet/EntityFrameworkCore/pull/12072 - Add DbFunction tests to the relational specification tests
  * Such that these tests can be run against all database providers
* https://github.com/aspnet/EntityFrameworkCore/pull/12362 - Async test cleanup
  * Remove `Wait` calls, unneeded async, and renamed some test methods
* https://github.com/aspnet/EntityFrameworkCore/pull/12666 - Unify logging test infrastructure
  * Added `CreateListLoggerFactory` and removed some previous logging infrastructure, which will require providers using these tests to react
* https://github.com/aspnet/EntityFrameworkCore/pull/12500 - Run more query tests both synchronously and asynchronously
  * Test names and factoring has changed, which will require providers using these tests to react
* https://github.com/aspnet/EntityFrameworkCore/pull/12766 - Renaming navigations in the ComplexNavigations model
  * Providers using these tests may need to react
* https://github.com/aspnet/EntityFrameworkCore/pull/12141 - Return the context to the pool instead of disposing in functional tests
  * This change includes some test refactoring which may require providers to react


#### Test and product code changes

* https://github.com/aspnet/EntityFrameworkCore/pull/12109 - Consolidate RelationalTypeMapping.Clone methods
  * Changes in 2.1 to the RelationalTypeMapping allowed for a simplification in derived classes. We don't believe this was breaking to providers, but providers can take advantage of this change in their derived type mapping classes.
* https://github.com/aspnet/EntityFrameworkCore/pull/12069 - Tagged or named queries
  * Adds infrastructure for tagging LINQ queries and having those tags show up as comments in the SQL. This may require providers to react in SQL generation.
* https://github.com/aspnet/EntityFrameworkCore/pull/13115 - Support spatial data via NTS
  * Allows type mappings and member translators to be registered outside of the provider
    * Providers must call base.FindMapping() in their ITypeMappingSource implementation for it to work
  * Follow this pattern to add spatial support to your provider that is consistent across providers.

