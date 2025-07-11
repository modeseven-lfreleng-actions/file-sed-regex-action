<!--
SPDX-License-Identifier: Apache-2.0
SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🔀 String Substitution in File (using sed)

Performs string substitutions using the command-line tool, GNU sed.

## file-sed-regex-action

## Usage Example

Call as a step in a larger composite action or workflow.

<!-- markdownlint-disable MD013 -->

```yaml
- name: 'Replace project version string'
  uses: lfreleng-actions/file-sed-regex-action@main
  with:
    flags: '-i -E'
    regex: 's/^version =.*$/version = "1.0.0"/;tx;q5;:x'
    path: 'pyproject.toml'
```

<!-- markdownlint-enable MD013 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Variable Name | Required | Default | Description                                     |
| ------------- | -------- | ------- | ----------------------------------------------- |
| flags         | True     | N/A     | The flags passed to sed on the command line     |
| regex         | True     | N/A     | The regular expression to use                   |
| path          | True     | N/A     | Path to the file to undergo string substitution |
| debug         | False    | false   | Enable debugging output                         |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Variable Name    | Description                                    |
| ---------------- | ---------------------------------------------- |
| exit_status      | The sed command exit status                    |

<!-- markdownlint-enable MD013 -->

## Implementation Details

Most sed implementations will not set exit status to a non-zero value and error
when a string substitution operation fails. GNU sed supports setting the exit
status by passing options in the substitution instruction:

`'s/^version =.*$/version = "1.0.0"/;tx;q5;:x'`

This example sets exit status to 5 if the version string substitution fails.

For this reason, the action checks that the version of sed on the runner is the
GNU version, as systems based typically on BSD may not support this feature.
