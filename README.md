# DirDelta

`dirdelta` is a small Bash utility that compares two directory trees and reports
regular files that are present in one tree but missing at the same relative path
in the other. It does not copy, modify, or delete any files.

## Usage

```bash
./dirdelta parentDir1 parentDir2
```

The script requires exactly two arguments.

## What It Does

Given two parent directories, the script:

1. Lists files in `parentDir1` that are missing from `parentDir2`.
2. Lists files in `parentDir2` that are missing from `parentDir1`.
3. Reports when one directory contains every file found in the other.

Files are compared by relative path, not by content. A file present at the same
relative path in both directories is treated as present even when its contents
differ. Hidden files are included in the comparison.

## Example

Before running the script:

```text
dir_1/
├── file_1.txt
├── file_2.txt
└── notes/today.txt

dir_2/
├── file_2.txt
├── file_3.txt
└── drafts/idea.txt
```

Run:

```bash
./dirdelta dir_1 dir_2
```

Output:

```text
Files not found in dir_2:
dir_1/file_1.txt
dir_1/notes/today.txt

-----------------

Files not found in dir_1:
dir_2/file_3.txt
dir_2/drafts/idea.txt
```

## Notes

- The script does not compare file contents.
