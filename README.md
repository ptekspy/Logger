# Logger

A small logger module with log levels, timestamp support, production toggles, and custom sinks.

## Getting Started

To build the package use:

```bash
argon build
```

Install the package with wally:

```bash
wally add ptekspy/Logger
```

## Usage

Require and use in your Luau code (adjust path as needed):

```lua
local Logger = require(path.to.Logger.init)

local logger = Logger.new("MyStore")
logger:Debug("starting", {count = 1})
logger:Info("loaded")
logger:Warn("missing value")
-- logger:Error("fatal") -- raises an error
```

### Configuration

```lua
local logger = Logger.new("Store", {
    enabled = true,
    level = "Info",
    timestamps = true,
    output = function(self, level, prefix, message)
        -- Custom sink, e.g. send to remote logger
        print("CUSTOM OUTPUT:", message)
    end,
})

logger:SetLevel("Warn")
logger:SetPrefix("NewStore")
logger:SetEnabled(false)
logger:SetTimestamps(true)
```

### Notes

- `Log` is an alias for `Info`
- `Debug`, `Info`, `Warn`, `Error` will only log when the current level allows it
- `Error` still raises an error so execution stops as expected
- `enabled` defaults to Studio mode unless explicitly configured otherwise
