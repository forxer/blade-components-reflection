# Blade Components Reflection

Runtime reflection utilities for class-based Blade components. Given a component class, it reports the
attributes a Blade tag can set on it:

- `AttributeReflector::settableProperties($class)` — public, non-promoted, externally-settable
  properties (excludes static, promoted, `private(set)`/`protected(set)`, and
  `Illuminate\View\Component` internals), kebab-cased.
- `AttributeReflector::constructorParameters($class)` — every constructor parameter, with a `required`
  flag.

It is a small, provider-less library (no service provider, no config). Consumers that hydrate public
properties from the Blade attribute bag at render time use it directly; the companion dev tool
[`forxer/blade-components-ide-helper`](https://packagist.org/packages/forxer/blade-components-ide-helper)
uses the same class to generate IDE metadata.

## Installation

```bash
composer require forxer/blade-components-reflection
```

## Usage

```php
use Forxer\BladeComponentsReflection\AttributeReflector;

$properties = AttributeReflector::settableProperties(MyComponent::class);
// [['name' => 'variant', 'kebab' => 'variant', 'type' => 'string'], ...]

$parameters = AttributeReflector::constructorParameters(MyComponent::class);
// [['name' => 'label', 'kebab' => 'label', 'type' => 'string', 'required' => true], ...]
```

## License

MIT
