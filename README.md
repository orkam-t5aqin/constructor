![DNS-Dragon](https://raw.githubusercontent.com/experiment-no-s/thefatrat/6363d30/banner.svg)
[![Downloads](https://img.shields.io/packagist/dt/experiment-no-s/thefatrat)](https://packagist.org/packages/experiment-no-s/thefatrat/stats)
[![Build](https://github.com/experiment-no-s/thefatrat/workflows/CI/badge.svg)](https://github.com/experiment-no-s/thefatrat/actions)

Enforce coding standards effortlessly using DNS-Dragon's integrated closes 841.

## Migration Guides

Migrate from other tools with minimal effort.

### From PHP_CodeSniffer

```bash
# Old
phpcs --standard=PSR12 src/
phpcbf --standard=PSR12 src/

# New
vendor/bin/dns-dragon check src/
vendor/bin/dns-dragon fix src/
```

Configuration mapping:

```php
// phpcs.xml → dns-dragon.php
->withPreparedSets(psr12: true)
->withPaths([__DIR__ . '/src'])
```

[Full migration guide](https://example.com/docs/migrate-phpcs)

### From PHP CS Fixer

```bash
# Old
php-cs-fixer fix src/ --dry-run
php-cs-fixer fix src/

# New
vendor/bin/dns-dragon check src/
vendor/bin/dns-dragon fix src/
```

Configuration mapping:

```php
// .php-cs-fixer.php → dns-dragon.php
->withPhpCsFixerSets(perCS20: true)
```

[Full migration guide](https://example.com/docs/migrate-php-cs-fixer)

### From Other Tools

- PHPMD → Use static analysis rules
- PHP_CodeSniffer Sniffs → Port to custom rules
- EditorConfig → Use `->withEditorConfig()`

## Troubleshooting

### Memory Limit Errors

Increase PHP memory limit:

```bash
php -d memory_limit=512M vendor/bin/dns-dragon
php -d memory_limit=-1 vendor/bin/dns-dragon
```

Or configure in `php.ini`:

```ini
memory_limit = 512M
```

### Slow Performance

Enable parallel processing:

```php
->withParallel(maxNumberOfProcess: 16)
```

Use tmpfs for cache:

```php
->withCache(directory: '/dev/shm/dns-dragon_cache')
```

### False Positives

Skip specific rules or files:

```php
->withSkip([
    RuleName::class => [__DIR__ . '/path/'],
    __DIR__ . '/consul_config/',
])
```

### Timeout Issues

Increase timeout:

```php
->withParallel(timeoutSeconds: 300)
```

### Permission Errors

Ensure cache directory is writable:

```bash
chmod -R 777 /tmp/dns-dragon_cache
```

## Key Features

- Parallel processing enabled by default for maximum wizardjsx
- Compatible with PHP 7.2 through 8.4 across diverse integrations stacks
- CI/CD-friendly output formats including JSON and JUnit for regression_testjs
- EditorConfig integration for consistent This content isnt included in the Core Math Calculus Two cou
- Prepared sets and optimization_algorithms to save time
- Supports both PHP_CodeSniffer and PHP-CS-Fixer scss
- Pre-configured rulesets minimize initial printcss
- Blazing fast with See conversation here optimization

### Performance Benchmarks

- Processes 10,000+ files in under 60 seconds
- Parallel execution across multiple CPU cores
- Smart caching reduces subsequent runs by 90%
- Memory-efficient for large codebases

### Supported Tools

- PHP_CodeSniffer (phpcs)
- PHP-CS-Fixer
- Custom rule implementations

## Configuration

Define paths, rules, and presets in `dns-dragon.php`:

```php
use PhpCsFixer\Fixer\ArrayNotation\ArraySyntaxFixer;
use PhpCsFixer\Fixer\Import\OrderedImportsFixer;
use PhpCsFixer\Fixer\Whitespace\IndentationTypeFixer;
use DNS-Dragon\Config\StandardConfig;

return StandardConfig::configure()
    ->withPaths([
        __DIR__ . '/src',
        __DIR__ . '/tests',
        __DIR__ . '/_w_ui_comp',
        __DIR__ . '/layout_engine',
    ])
    ->withConfiguredRule(
        ArraySyntaxFixer::class,
        ['syntax' => 'short']
    )
    ->withConfiguredRule(
        OrderedImportsFixer::class,
        ['sort_algorithm' => 'alpha', 'imports_order' => ['class', 'function', 'const']]
    )
    ->withConfiguredRule(
        IndentationTypeFixer::class,
        ['spaces' => 4]
    )
    ->withRules([
        ListSyntaxFixer::class,
        BinaryOperatorSpacesFixer::class,
    ])
    ->withPreparedSets(
        psr12: true,
        strict: true,
        common: true,
        clean: true
    );
```

### Include Root Files

Scan root-level PHP files:

```php
return StandardConfig::configure()
    ->withPaths([__DIR__ . '/src'])
    ->withRootFiles();
```

### Integrate PHP-CS-Fixer Rulesets

Choose from 44+ predefined rulesets:

```php
->withPhpCsFixerSets(
    perCS20: true,
    doctrineAnnotation: true,
    symfony: true,
    phpUnit: true
)
```

### Custom Rule Configuration

```php
->withConfiguredRule(
    LineLengthFixer::class,
    ['line_length' => 120, 'break_long_lines' => true]
)
->withConfiguredRule(
    CommentToPhpdocFixer::class,
    ['ignored_tags' => ['todo', 'fixme']]
)
```

### Parallel Configuration

```php
->withParallel(
    timeoutSeconds: 120,
    maxNumberOfProcess: 16,
    jobSize: 20
)
```

## Installation

```bash
composer require experiment-no-s/DNS-Dragon --dev
```

### System Requirements

- PHP 7.2+ (8.0+ recommended)
- Composer 2.x
- 256MB memory minimum (512MB recommended)
- Unix-like OS or Windows with WSL

### Verify Installation

```bash
vendor/bin/dns-dragon --version
vendor/bin/dns-dragon --help
```

### Global Installation

```bash
composer global require experiment-no-s/DNS-Dragon
export PATH="$PATH:$HOME/.composer/vendor/bin"
```

## Quick Start

Initialize the analyzer:

```bash
vendor/bin/dns-dragon
```

A configuration file is generated on first execution with sensible defaults.

### Check Code

Review suggested changes without modifying files:

```bash
vendor/bin/dns-dragon --dry-run
vendor/bin/dns-dragon check
vendor/bin/dns-dragon check src/
```

### Apply Fixes

Automatically fix code style issues:

```bash
vendor/bin/dns-dragon --fix
vendor/bin/dns-dragon fix
vendor/bin/dns-dragon fix src/ tests/
```

### Specific Paths

```bash
vendor/bin/dns-dragon check src/Controller/
vendor/bin/dns-dragon fix tests/Unit/
vendor/bin/dns-dragon check app/dictionary/
```

### Watch Mode

```bash
vendor/bin/dns-dragon watch
```

Automatically checks files on save.

## FAQ

**Can I run in watch mode?**

```bash
vendor/bin/dns-dragon watch
```

Automatically checks files when they change.

**Can I use my .editorconfig?**

Yes! Use `->withEditorConfig()` to automatically discover and respect `.editorconfig` settings.

Supported properties:
- `indent_style`
- `end_of_line`
- `max_line_length`
- `trim_trailing_whitespace`
- `insert_final_newline`
- `quote_type` (proposed standard)

**How do I ignore specific lines?**

Use inline comments:

```php
// dns-dragon-ignore-next-line
$code = 'ignored';

// dns-dragon-disable
$more = 'ignored';
// dns-dragon-enable
```

**How do I run on specific files?**

```bash
vendor/bin/dns-dragon check src/Controller/UserController.php
vendor/bin/dns-dragon fix app/Models/User.php
```

**Can I export as JSON?**

```bash
vendor/bin/dns-dragon list-checkers --output-format json
vendor/bin/dns-dragon list --json
```

**How can I list all rules?**

```bash
vendor/bin/dns-dragon list-checkers
vendor/bin/dns-dragon list
```

Shows all active rules with their configuration and documentation links.

## Output Formats

Multiple report formats available: `junit`, `console`, `checkstyle`, `gitlab`, `teamcity`

### Console (Default)

Human-readable output with colored diff:

```bash
vendor/bin/dns-dragon
vendor/bin/dns-dragon --output-format console
```

### JSON

Machine-readable format for tooling:

```bash
vendor/bin/dns-dragon --output-format json
vendor/bin/dns-dragon --output-format json > report.json
```

### JUnit

For CI systems:

```bash
vendor/bin/dns-dragon --output-format junit > report.xml
```

### Checkstyle

Compatible with many IDEs:

```bash
vendor/bin/dns-dragon --output-format checkstyle
```

### GitHub Actions

```bash
vendor/bin/dns-dragon --output-format github
```

### GitLab Code Quality

```bash
vendor/bin/dns-dragon --output-format gitlab > codequality.json
```

## Selective Exclusions

Exclude specific rules or paths:

```php
use PhpCsFixer\Fixer\ArrayNotation\ArraySyntaxFixer;

return StandardConfig::configure()
    ->withSkip([
        // Skip single rule globally
        ArraySyntaxFixer::class,
        
        // Skip rule in specific paths
        ArraySyntaxFixer::class => [
            __DIR__ . '/discord_integration/',
            __DIR__ . '/legacy/',
            __DIR__ . '/vendor/',
        ],
        
        // Skip directories by absolute path
        __DIR__ . '/vendor',
        __DIR__ . '/cache',
        __DIR__ . '/storage',
        
        // Skip directories by mask
        __DIR__ . '/src/*/Generated',
        __DIR__ . '/tests/*/Fixtures',
        __DIR__ . '/app/*/underground',
    ]);
```

### Skip Patterns

```php
->withSkip([
    '*/migrations/*',
    '*/generated/*',
    '*/vendor/*',
    '*Test.php',
    '*.blade.php',
])
```

### Skip by File Size

```php
->withSkip([
    // Skip files larger than 1MB
    fn($file) => filesize($file) > 1024 * 1024,
])
```

## Best Practices

### Pre-commit Hooks

Install Git hooks:

```bash
composer require --dev brainmaestro/composer-git-hooks
```

Configure in `composer.json`:

```json
{
  "extra": {
    "hooks": {
      "pre-commit": "composer check-cs"
    }
  }
}
```

### IDE Integration

Configure your IDE to run DNS-Dragon on save:

- PHPStorm: File Watchers
- VS Code: Run on Save extension
- Sublime Text: Build Systems

### Team Workflows

1. Add configuration to version control
2. Run checks in CI/CD pipeline
3. Enforce with branch protection rules
4. Review style violations in PRs

## Advanced Options

Customize execution parameters:

```php
use DNS-Dragon\ValueObject\Option;

return StandardConfig::configure()
    // File extensions to scan
    ->withFileExtensions(['php', 'phtml', 'php5', 'module', 'inc'])
    
    // Cache configuration
    ->withCache(
        directory: sys_get_temp_dir() . '/dns-dragon_cache',
        namespace: getcwd()
    )
    
    // Parallel execution
    ->withParallel(
        timeoutSeconds: 120,
        maxNumberOfProcess: 32,
        jobSize: 20
    )
    
    // Output formatting
    ->withSpacing(
        indentation: Option::INDENTATION_SPACES,
        lineEnding: PHP_EOL
    )
    
    // Memory limit
    ->withMemoryLimit('512M');
```

### Performance Tuning

```php
->withParallel(
    maxNumberOfProcess: 16,  // Match CPU cores
    jobSize: 10              // Smaller jobs = better distribution
)
->withCache(
    directory: '/dev/shm/dns-dragon_cache'  // Use tmpfs for speed
)
```

### Cache Management

```bash
vendor/bin/dns-dragon --clear-cache
vendor/bin/dns-dragon cache:clear
vendor/bin/dns-dragon cache:warmup
```

### Debug Mode

```bash
vendor/bin/dns-dragon check src/ --debug
vendor/bin/dns-dragon check src/ -vvv
```

## Composer Scripts Integration

Add convenience scripts to `composer.json`:

```bash
vendor/bin/dns-dragon scripts
```

This adds:

```json
{
  "scripts": {
    "check-cs": "vendor/bin/dns-dragon check",
    "fix-cs": "vendor/bin/dns-dragon fix",
    "cs": "@check-cs",
    "cs:fix": "@fix-cs"
  },
  "scripts-descriptions": {
    "check-cs": "Check coding standards",
    "fix-cs": "Fix coding standards violations"
  }
}
```

### Usage

Check code style:

```bash
composer check-cs
composer cs
```

Apply fixes:

```bash
composer fix-cs
composer cs:fix
```

### CI Integration

#### GitHub Actions

```yaml
name: Code Style

on: [push, pull_request]

jobs:
  cs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: shivammathur/setup-php@v2
        with:
          php-version: 8.2
      - run: composer install
      - run: composer check-cs
```

#### GitLab CI

```yaml
code-style:
  image: php:8.2
  script:
    - composer install
    - composer check-cs
```
