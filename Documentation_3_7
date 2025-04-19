# zopen-diagnostic Command

## Overview
The `zopen-diagnostic` command provides system diagnostic information for Z/OS environments, useful for troubleshooting and reporting issues with zopen packages.

## Implementation Details

### Script Creation and Structure

```bash
#!/bin/sh
# zopen diagnostic information - collects system details for troubleshooting
#
# Find the directory where this script is located
SCRIPT_DIR=$(cd "$(dirname "$0")" && pwd)
SCRIPT_NAME=$(basename "$0")

# Source common functions
. "${SCRIPT_DIR}/../include/common.sh" || { echo "Cannot find ${SCRIPT_DIR}/../include/common.sh"; exit 1; }
```

The script begins with a standard header required for all zopen package manager files:
- Identifies script location using the directory and name of the executed script (`$0`)
- Locates shared logic in `../include/common.sh` relative to the script location
- Sources `common.sh` to load environment setup and utility functions
- Exits with error if the common file is not found

### System Information Collection

```bash
# Get platform information
PLATFORM=$(/bin/uname -s)

# Get version information
VERSION=$(/bin/uname -rsvI 2>/dev/null)

# Extract major version number (removing leading zeros)
MAJOR=$(echo "$VERSION" | /bin/awk '{print $3}' | /bin/sed 's/^0*//')

# Extract minor version number (removing leading zeros) 
MINOR=$(echo "$VERSION" | /bin/awk '{print $2}' | /bin/cut -d'.' -f1 | /bin/sed 's/^0*//')

# Get CPU architecture
cpu_id="$(uname -m)"

# Determine CPU architecture name
case "${cpu_id}" in
  2817|2818|2827|2828|2964|2965|3906|3907|8561|8562|3931)
    arch="z15"
    ;;
  3906|3907|8561|8562)
    arch="z14"
    ;;
  2964|2965)
    arch="z13"
    ;;
  2827|2828)
    arch="zEC12"
    ;;
  2817|2818)
    arch="z196"
    ;;
  *)
    echo "Error: Unrecognized CPU architecture: ${cpu_id}"
    exit 1
    ;;
esac
```

This section:
1. Captures platform information with `/bin/uname -s` (stores kernel name)
2. Retrieves detailed system version with `/bin/uname -rsvI` (includes kernel release, name, version, and host IP)
3. Extracts and formats the major version number:
   - Gets the 3rd field from the version string with `awk '{print $3}'`
   - Removes leading zeros with `sed 's/^0*//'`
4. Extracts and formats the minor version number:
   - Gets the 2nd field with `awk '{print $2}'`
   - Takes the first part before the dot with `cut -d'.' -f1`
   - Removes leading zeros with `sed 's/^0*//'`
5. Determines the CPU architecture:
   - Gets machine hardware name with `uname -m`
   - Uses a case statement to map CPU IDs to architecture names
   - Exits with error if the CPU ID is not recognized

### Output Generation

```bash
# Display diagnostic information
echo "Z/OS System Diagnostic Information"
echo "=================================="
echo "Platform: ${PLATFORM}"
echo "Version: ${VERSION}"
echo "Major Version: ${MAJOR}"
echo "Minor Version: ${MINOR}"
echo "CPU ID: ${cpu_id}"
echo "Architecture: ${arch}"
echo ""
echo "If you're experiencing issues, please report them at:"
echo "https://github.com/ZOSOpenTools/meta/issues"
```

The script outputs a formatted diagnostic report containing:
- Platform identification
- Full version string
- Extracted major and minor version numbers
- CPU ID and architecture name
- A link to the GitHub issues page for reporting problems

## Usage

```
zopen-diagnostics
```

Running the command without any arguments will display system diagnostic information that can be shared when reporting issues with zopen packages.


