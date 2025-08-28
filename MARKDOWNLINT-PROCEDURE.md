# Markdownlint Check Procedure

## **MANDATORY PRE-COMMIT CHECKLIST**

Before any `git commit` and `git push`, **ALWAYS** run these checks:

### **1. Run Complete Markdownlint Check**
```bash
markdownlint **/*.md
```

### **2. Fix Critical Violations IMMEDIATELY**
If you see any of these violations, fix them before committing:

#### **Critical Rules (MUST FIX):**
- **MD047**: Files should end with a single newline character
- **MD009**: No trailing spaces
- **MD026**: No trailing punctuation in headings
- **MD034**: No bare URLs (wrap in angle brackets `<url>`)

#### **Important Rules (SHOULD FIX):**
- **MD022**: Headings should be surrounded by blank lines
- **MD032**: Lists should be surrounded by blank lines
- **MD031**: Fenced code blocks should be surrounded by blank lines

### **3. Remove Non-Markdown Files**
```bash
# Check for unwanted files
find . -type f ! -name "*.md" ! -path "./.git/*" ! -name ".gitignore"

# Remove any .sh, .py, or other script files
rm -f *.sh *.py *.js *.json *.txt
```

### **4. Quick Fix Commands**

#### **Fix MD047 (Missing final newline):**
```bash
# Add newline to all .md files that don't end with one
find . -name "*.md" -exec sh -c 'test "$(tail -c1 "$1")" && echo "" >> "$1"' _ {} \;
```

#### **Fix MD009 (Trailing spaces):**
```bash
# Remove trailing spaces from all .md files
find . -name "*.md" -exec sed -i '' 's/[[:space:]]*$//' {} \;
```

#### **Fix MD026 (Trailing punctuation in headings):**
```bash
# Remove trailing punctuation from headings
find . -name "*.md" -exec sed -i '' -E 's/^(#+[[:space:]]+.*[^[:space:]])[.!?:;]+[[:space:]]*$/\1/' {} \;
```

### **5. Final Verification**
```bash
# Run markdownlint one more time to confirm fixes
markdownlint **/*.md

# If no output, you're ready to commit!
```

## **Standard Markdownlint Rules Reference**

### **Critical Rules (Zero Tolerance)**
- `MD047` - single-trailing-newline: Files should end with a single newline character
- `MD009` - no-trailing-spaces: Trailing spaces
- `MD026` - no-trailing-punctuation: Trailing punctuation in heading
- `MD034` - no-bare-urls: Bare URL used

### **Important Rules (Fix When Possible)**
- `MD022` - blanks-around-headings: Headings should be surrounded by blank lines
- `MD032` - blanks-around-lists: Lists should be surrounded by blank lines
- `MD031` - blanks-around-fences: Fenced code blocks should be surrounded by blank lines
- `MD012` - no-multiple-blanks: Multiple consecutive blank lines

### **Optional Rules (Documentation Standards)**
- `MD013` - line-length: Line length (can be ignored for technical documentation)
- `MD041` - first-line-heading: First line in file should be a top-level heading
- `MD036` - no-emphasis-as-heading: Emphasis used instead of a heading

## **Git Workflow with Markdownlint**

### **Before Every Commit:**
```bash
# 1. Run markdownlint check
markdownlint **/*.md

# 2. Fix any violations (use commands above)

# 3. Remove unwanted files
rm -f *.sh *.py *.js *.json

# 4. Verify clean status
markdownlint **/*.md

# 5. Commit only if no violations
git add -A
git commit -m "Your commit message"
git push
```

### **Emergency Fix Script**
If you need a quick fix for all critical issues:

```bash
#!/bin/bash
# Fix critical markdownlint issues

echo "🔧 Fixing critical markdownlint issues..."

# Fix MD047: Add final newlines
find . -name "*.md" -exec sh -c 'test "$(tail -c1 "$1")" && echo "" >> "$1"' _ {} \;

# Fix MD009: Remove trailing spaces
find . -name "*.md" -exec sed -i '' 's/[[:space:]]*$//' {} \;

# Fix MD026: Remove trailing punctuation from headings
find . -name "*.md" -exec sed -i '' -E 's/^(#+[[:space:]]+.*[^[:space:]])[.!?:;]+[[:space:]]*$/\1/' {} \;

# Remove script and temp files
rm -f *.sh *.py *.js *.json *.txt *.log

echo "✅ Critical fixes applied. Run 'markdownlint **/*.md' to verify."
```

## **Integration with CI/CD**

For automated checking, add this to your CI pipeline:
```yaml
- name: Lint Markdown files
  run: |
    npm install -g markdownlint-cli
    markdownlint **/*.md
```

## **Summary**

**REMEMBER**:
- ✅ **Always** run `markdownlint **/*.md` before committing
- ✅ **Always** remove non-.md files before committing
- ✅ **Always** fix MD047, MD009, MD026, MD034 violations
- ✅ **Never** commit with critical markdownlint violations
