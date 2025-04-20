# zopen-diagnostic Command Enhancement Update

## Summary of Changes
Today, I added functionality requested by Igor to the `zopen-diagnostic` command:

1. Added disk space usage reporting
2. Enhanced issue reporting URL functionality

## Disk Space Usage Reporting
I implemented new functionality that displays:
- Total disk space used by zopen
- Directory location where the tool is mounted

### Implementation Details:
- Used `du -sh "$ZOPEN_ROOTFS"` to find disk space usage
  - `du` prints disk usage of specified arguments
  - `-s` flag sums all disk usage
  - `-h` flag displays results in human-readable format (MB, GB, etc.)
- Used `df -h "$ZOPEN_ROOTFS"` to display free disk space
  - This shows available storage space across the system in human-readable format

## Issue Reporting Enhancement
I added logic to make the issue reporting URL more intelligent:

- The command now checks if an argument was passed
- If no argument is provided, it redirects to the general package manager issue page
- If an argument is provided:
  - Uses `cut -d ' ' -f2 | tr -d' '` to trim all spaces from the arguments
  - Modifies the URL to direct users to the correct tool-specific repository for issue reporting
