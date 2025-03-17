<!--
SPDX-License-Identifier: Apache-2.0
SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 📦 String Substitution in File (using sed)

Performs string substitutions using the command-line tool, sed.

## file-sed-regex-action

## Usage Example

Call as a step in a larger composite action or workflow.

<!-- markdownlint-disable MD013 -->

```yaml
- name: "Replace project version string"
  uses: lfreleng-actions/file-sed-regex-action@main
  with:
    flags: "-i -E"
    regex: 's:^version =.*$:version = "${{ env.REPLACEMENT_STRING }}":'
    path: "pyproject.toml"
```

<!-- markdownlint-enable MD013 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Variable Name | Required | Default | Description                                            |
| ------------- | -------- | ------- | ------------------------------------------------------ |
| FLAGS         | True     | N/A     | The flags passed to sed on the command line            |
| REGEX         | True     | N/A     | The regular expression to use                          |
| PATH          | True     | N/A     | Path to the file to undergo string substitution        |
| NO_FAIL       | False    | False   | Do not exit (when file not found or replacement fails) |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Variable Name    | Description                                    |
| ---------------- | ---------------------------------------------- |
| EXIT_STATUS      | The sed command exit status                    |

Note: output variable will be inaccessible unless NO_FAIL provided as input to the action

<!-- markdownlint-enable MD013 -->
