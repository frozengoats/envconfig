# envconfig
configure your application from the environment

```
  import (
    "time"
    "github.com/frozengoats/envconfig"
  )

  var config struct {
    NumCores  int           `env:"APP_CPU_CORES" default:"4"`
    Fractions float64       `env:"APP_FRACTIONS" default:"2.7"`
    Interval  time.Duration `env:"APP_DURATION" default:"3h"`
    Enabled   bool          `env:"APP_ENABLED" default:"false"`
    Name      string        `env:"APP_NAME"`
  }

  err := envconfig.Apply(&config)
```

all variants of int/float are supported as field data types.

for durations, the following are supported in order from largest to smallest
- `w` week
- `d` day
- `h` hour
- `m` minute
- `s` second
- `ms` millisecond
- `us` microsecond
- `ns` nanosecond

for booleans, the following variants are recognized
- `f`, `false`, `0` for false
- `t`, `true`, `1` for true
- case is insensitive

enforcement of required configuration variables is accomplished as follows
```
err := envconfig.Apply(&config, WithErrorOnMissing())
```
in this case, err will be set when any environment variable is not set, that also does not contain a `default` directive.