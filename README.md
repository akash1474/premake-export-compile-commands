# Premake: Generate compile_commands.json

A Premake 5 script that generates a `compile_commands.json` file for your C/C++ projects. This file is used by a wide range of tools, including language servers (like Clangd) and static analyzers, to understand your project's structure and build options.

## Features

- **Easy to Configure:** No need to dig through the code. Key settings are available as constants at the top of the script.
- **Clean & Valid Output:** Generates a single, well-formatted `compile_commands.json` file.
- **Customizable Build Flags:** Easily specify the C++ standard and add any additional compiler flags you need.
- **Folder Exclusion:** Keep your compilation database clean by excluding vendor libraries, build directories, or other non-project folders.

## Installation

1.  Clone or download the `compiledb.lua` script. A good practice is to place it in a common scripts directory. For example:

    ```bash
    # You can place the script in a central location for premake to find
    mkdir -p ~/.premake
    # Now, move the compiledb.lua script into ~/.premake/
    ```

2.  Require the script in  `compiledb.lua` file in your system-wide `premake-system.lua` file.
    ```lua
    -- In your premake5.lua
    require "compiledb"
    ```

## Usage

Once the script is setup globally, you can generate the compilation database by running the `compiledb` action from your terminal:

```bash
premake5 compiledb
```

This will create a `compile_commands.json` file in your project's root directory.



## Configuration

You can easily customize the script's behavior by editing the **Configuration Constants** section at the top of the `compiledb.lua` file.

```lua
--
-- Configuration Constants
--
local CPP_STANDARD = "c++17"
local IGNORE_FOLDERS = { "packages", "vendor", "build" }
local ADDITIONAL_COMMANDS = { "-Wall", "-Wextra" }
```

**`CPP_STANDARD`**: A string that specifies the C++ standard to be used (e.g., "c++17", "c++20"). This will be added to the compile commands as `-std=c++17`.

**`IGNORE_FOLDERS`**: A list of folder names to exclude from the compilation database. Any file path containing one of these strings will be ignored. This is perfect for filtering out third-party libraries or build artifacts.

**`ADDITIONAL_COMMANDS`**: A list of extra flags to add to every compile command. This is a great place to add warning flags like `-Wall` or project-specific defines.
