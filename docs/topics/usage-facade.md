# Facade

> To use this functionality, make sure you have the [`%package-locales%`](packages-locales.md) package installed.
>
{style="note"}

To work with locales, you can use the facade `LaravelLang\Locales\Facades\Locales`.
It allows you to receive information in two ways: a list of locale codes or an array of DTO objects.

## Data objects

```php
use LaravelLang\Locales\Facades\Locales;

// List of available localizations.
Locales::available(): array // array<LocaleData>

// List of installed localizations.
Locales::installed(bool $withProtects = true): array // array<LocaleData>

// List of uninstalled localizations.
Locales::notInstalled(): array // array<LocaleData>

// Retrieving a list of protected locales.
Locales::protects(): array // array<LocaleData>

// Check if language packs are available in requested locale.
Locales::isAvailable(Locale|string|null $locale): bool

// Check if a language pack is installed.
Locales::isInstalled(Locale|string|null $locale): bool

// The checked locale protecting.
Locales::isProtected(Locale|string|null $locale): bool

// Validate and returns the correct localization.
// If an uninstalled localization is requested, then it will return the currently active one in the application.
Locales::get(mixed $locale): LocaleData

// Getting the default localization name.
Locales::getDefault(): LocaleData

// Getting the fallback localization name.
Locales::getFallback(): LocaleData

// Receives information about any available localization, otherwise it will return the currently active one in the application.
Locales::info(mixed $locale): LocaleData
```

## Raw data

```php
use LaravelLang\Locales\Enums\Locale;
use LaravelLang\Locales\Facades\Locales;

// List of available localizations.
Locales::raw()->available(): array // array<string>

// List of installed localizations.
Locales::raw()->installed(bool $withProtects = true): array // array<string>

// List of uninstalled localizations.
Locales::raw()->notInstalled(): array // array<string>

// Retrieving a list of protected locales.
Locales::raw()->protects(): array // array<string>

// Check if language packs are available in requested locale.
Locales::raw()->isAvailable(Locale|string|null $locale): bool

// Check if a language pack is installed.
Locales::raw()->isInstalled(Locale|string|null $locale): bool

// The checked locale protecting.
Locales::raw()->isProtected(Locale|string|null $locale): bool

// Validate and returns the correct localization.
// If an uninstalled localization is requested, then it will return the currently active one in the application.
Locales::raw()->get(mixed $locale): string

// Getting the default localization name.
Locales::raw()->getDefault(): string

// Getting the fallback localization name.
Locales::raw()->getFallback(): string

// Receives locale code for any available localization, otherwise it will return the currently active one in the application.
Locales::raw()->info(mixed $locale): string
```

## Examples

```php
use LaravelLang\Locales\Data\LocaleData;
use LaravelLang\Locales\Facades\Locales;

// config('app.locale') // de

return Locales::getDefault();

// Non aliased
LocaleData {
  +code: "de"
  +type: "Latn"
  +name: "German"
  +native: "Deutsch"
  +localized: "Deutsch"
  +regional: "de_DE"
  +orientation: "left-to-right"
}

// Aliased
LocaleData {
  +code: "de-DE"
  +type: "Latn"
  +name: "German"
  +native: "Deutsch"
  +localized: "Deutsch"
  +regional: "de_DE"
  +orientation: "left-to-right"
}
```

```php
use LaravelLang\Locales\Data\LocaleData;
use LaravelLang\Locales\Facades\Locales;

// config('app.locale') // vi

return Locales::get('de');

LocaleData {
  +code: "de"
  +type: "Latn"
  +name: "German"
  +native: "Deutsch"
  +localized: "Tiếng Đức"
  +regional: "de_DE"
  +orientation: "left-to-right"
}

LocaleData {
  +code: "ar"
  +type: "Arab"
  +name: "Arabic"
  +native: "العربية"
  +localized: "Tiếng Ả Rập"
  +regional: "ar_AE"
  +orientation: "right-to-left"
}
```

```php
use LaravelLang\Locales\Data\LocaleData;
use LaravelLang\Locales\Facades\Locales;

// config('app.locale') // de

return Locales::get('foo');

// Will return the default locale
LocaleData {
  +code: "de"
  +type: "Latn"
  +name: "German"
  +native: "Deutsch"
  +localized: "Deutsch"
  +regional: "de_DE"
  +orientation: "left-to-right"
}
```

```php
return Locales::raw()->getDefault();
// Non aliased
// de

// Aliased
// de-DE
```

```php
return Locales::raw()->get('de');
// de

return Locales::raw()->get('foo');
// Will return the default locale
// de
```