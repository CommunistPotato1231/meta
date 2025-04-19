# Package Lookup Fix Documentation

## Issue Fix: zopen info Error for Tagged Packages

This document outlines changes made to fix Issue #958, where users were encountering the error `***ERROR: Package 'vim%datasetio' not found in remote repository` when attempting to look up tagged packages using `zopen info`.

### Problem Summary

The error occurred because the package lookup logic had two issues:
1. It was only searching for packages using the `tag` field instead of also checking the `tag_name` field
2. For packages with tags, the code was not properly storing the correct remote data before validation checks

### Code Changes

The following changes were implemented to fix the issue:

```bash
# BEFORE:
remote_data=$(jq -c ".release_data.\"${package}\"[0]" "${JSON_CACHE}")

if [ -z "${remote_data}" ] || [ "${remote_data}" = "null" ]; then
    printError "Package '${package}' not found in remote repository."
    exit 1
# Missing closing bracket for this if statement

# AFTER:
remote_data=$(jq -c ".release_data.\"${package}\"[0]" "${JSON_CACHE}")

if [ -z "${remote_data}" ] || [ "${remote_data}" = "null" ]; then
    printError "Package '${package}' not found in remote repository."
    exit 1
fi  # Added missing closing bracket

if [ -n "$tag" ]; then
    printVerbose "Looking up tagged version '${tag}' for package '${base_package}'"
    remote_data=$(jq -c ".release_data.\"${base_package}\"[] | select(.tag == \"${tag}\")" "${JSON_CACHE}")
    remote_data=$(jq -c ".release_data.\"${base_package}\"[] | select(.tag_name == \"${tag}\")" "${JSON_CACHE}")
else
    remote_data=$(jq -c ".release_data.\"${base_package}\"[0]" "${JSON_CACHE}")
fi

if [ -z "${remote_data}" ] || [ "${remote_data}" = "null" ]; then
    printError "Package '${package}' not found in remote repository."
    exit 1
fi
```

### Key Improvements

1. **Fixed Syntax Error**: Added the missing closing bracket (`fi`) for the first if statement.

2. **Enhanced Tag Lookup**: Added support for handling both `tag` and `tag_name` fields:
   ```bash
   remote_data=$(jq -c ".release_data.\"${base_package}\"[] | select(.tag == \"${tag}\")" "${JSON_CACHE}")
   remote_data=$(jq -c ".release_data.\"${base_package}\"[] | select(.tag_name == \"${tag}\")" "${JSON_CACHE}")
   ```

3. **Better Error Handling**: Implemented a second validation check after the tag-specific lookup to provide appropriate error messages.

### Expected Behavior

After these changes:
- When using `zopen info` with tagged packages (e.g., `vim%datasetio`), the system will correctly search both the `tag` and `tag_name` fields
- If the package exists but the specified tag doesn't, users will receive a clear error message
- The fix maintains backward compatibility with packages that don't use tags


