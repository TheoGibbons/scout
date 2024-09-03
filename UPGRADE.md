# Upgrade Guide

## Upgrading To 11.0 From 10.x

### Algolia Engine V4 Support

In Scout 11.x, the Algolia engine has been updated to support Algolia V4. As a result, support for Algolia V3 has been removed, making this a breaking change. If you are currently using Algolia V3, you will need to upgrade to V4 to continue using the Algolia engine in Scout.

#### Key Changes:
- Removed support for Algolia V3.
- Added support for Algolia V4.
- PHP 8.1 or higher is required for compatibility with Algolia V4.

To use Algolia V4, you must update your `composer.json` file to include the following dependency:

```json
"algolia/algoliasearch-client-php": "^4.3"
```

Please review these changes carefully and ensure your application is compatible with the new requirements before upgrading.

### Algolia Engine `filters`

PR: https://github.com/laravel/scout/pull/839

In previous Scout releases, the Algolia engine utilized `numericFilters` to power `where` conditions. However, `numericFilters` does not support simple string matching. In Scout 11.x, `filters` is now used instead of `numericFilters`.

### Meilisearch Engine `scout:delete-all-indexes` Command

In previous releases, the Meilisearch engine’s `scout:delete-all-indexes` command would drop all indexes from the Meilisearch server. In Scout 11.x, the command now only drops indexes with the application's currently configured Scout prefix. Typically, this corresponds to the `SCOUT_PREFIX` environment variable and / or the `scout.prefix` configuration value.

## Upgrading To 10.0 From 9.x

### Minimum Versions

The following dependency versions have been updated:

- The minimum PHP version is now v8.0
- The minimum Laravel version is now v9.0

### The `getScoutKeyName` Method

PR: https://github.com/laravel/scout/pull/509

In Scout 10.x, the `getScoutKeyName` method will return the unqualified key name and no longer qualifies the key name with the table name. If your application is overriding the `getScoutKeyName` method you should ensure an unqualified key name is returned.

```diff
public function getScoutKeyName()
{
-    return 'posts.id';
+    return 'id';
}
```

### Removal Of `getUnqualifiedScoutKeyName`

PR: https://github.com/laravel/scout/pull/657

Due to the `getScoutKeyName` change discussed above, the `getUnqualifiedScoutKeyName` method was removed as it is no longer necessary.

### Meilisearch 1.0

Scout 10.x requires Meilisearch PHP 1.0 as its minimum supported SDK version; therefore, you should upgrade your dependency via your application's `composer.json` file:

```json
"meilisearch/meilisearch-php": "^1.0",
```

In this SDK update, all namespace and class references to "MeiliSearch" have been updated to "Meilisearch". Please review your code for any reference to the old capitalization and update those references accordingly.

In addition, please consult the full [Meilisearch PHP v1.0 changelog](https://github.com/meilisearch/meilisearch-php/releases/tag/v1.0.0) for further details.

## Upgrading To 9.0 From 8.x

### Minimum Laravel Version

Laravel 8.0 is now the minimum supported version of the framework.

### Minimum PHP Version

PHP 7.3 is now the minimum supported version of the language.

## Upgrading To 8.0 From 7.x

### Minimum Laravel Version

Laravel 6.0 is now the minimum supported version of the framework.

### Minimum PHP Version

PHP 7.2 is now the minimum supported version of the language.

## Upgrading To 7.0 From 6.x

### Updating Dependencies

Update your `laravel/scout` dependency to `^7.0` in your `composer.json` file.

### Algolia Driver

If you are using Algolia as your search provider, update your `algolia/algoliasearch-client-php` dependency to `^2.2` in your `composer.json` file.

#### Exception Renaming

The `AlgoliaSearch\AlgoliaException` exception class was renamed to `Algolia\AlgoliaSearch\Exceptions\AlgoliaException`.

#### The `search` Method Callback

If you are passing a callback to the `search` method, the callback will now receive an instance of `Algolia/AlgoliaSearch/SearchIndex` as its first argument.

#### Misc.

If you are using the Algolia API client directly, consider reviewing the [full changelog provided by Algolia](https://github.com/algolia/algoliasearch-client-php/blob/master/docs/UPGRADE-from-v1-to-v2.md).
