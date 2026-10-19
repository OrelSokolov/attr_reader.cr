# attr_reader.cr

Ruby-compat `attr_reader` / `attr_writer` / `attr_accessor` macros for
Crystal — Rails-style declarations with **zero dependencies**.

Extracted from
[active_support.cr](https://github.com/OrelSokolov/active_support.cr) so
low-level shards can use Rails-style attribute declarations without pulling
in `pg`/`redis` transitively.

## Usage

```crystal
require "attr_reader_cr"

class User
  attr_reader :body, :content_type          # Ruby-style symbols
  attr_accessor name : String = "anon"      # typed declaration with default
  attr_writer :secret                       # generates secret=
end
```

## Mapping

| Ruby               | idiomatic Crystal | attr_reader.cr   |
|--------------------|-------------------|------------------|
| `attr_reader :foo` | `getter foo`      | `attr_reader :foo` |
| `attr_writer :foo` | `setter foo`      | `attr_writer :foo` |
| `attr_accessor :foo` | `property foo`  | `attr_accessor :foo` |

All forms delegate to the stdlib `getter`/`setter`/`property` macros, so
typed declarations and defaults pass straight through:

```crystal
attr_accessor name : String = "anon", level : Int32 = 0
```

## Installation

1. Add the dependency to `shard.yml`:

   ```yaml
   dependencies:
     attr_reader_cr:
       github: OrelSokolov/attr_reader.cr
       version: ~> 0.1.0
   ```

2. Run `shards install`

## License

MIT
