# Shell and CLI Command Standards

All shell and CLI commands in code, scripts, and documentation must use long-form options to ensure clarity and readability for all users, including beginners.

## Rule

- **Use long-form options only, never short forms**
- Applies to: git, bash, sh, and all CLI tools
- Purpose: Improve readability and reduce ambiguity

## Examples

### git

✅ **Good:**

```bash
git commit --message "feat: add new feature"
git branch --list
git checkout --branch main
```

❌ **Bad:**

```bash
git commit -m "feat: add new feature"
git branch -l
git checkout -b main
```

### Other Tools

✅ **Good:**

```bash
grep --recursive --ignore-case --include="*.md" "search term"
```

❌ **Bad:**

```bash
grep -r -i --include="*.md" "search term"
```

## Notes

- This standard applies to documentation, scripts, code comments, and all examples
- Users who check out this repository should be able to understand and run commands without prior knowledge
- Where a tool provides no long form, use its documented form. `find` is the
  common case: `-type` and `-name` are the only forms it has.
