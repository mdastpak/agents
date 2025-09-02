# AI Agent Framework - Commit Rules

## **🚨 MANDATORY PRE-COMMIT CHECKLIST**

**EVERY commit and push MUST follow these rules. NO EXCEPTIONS.**

### **📋 Pre-Commit Verification (Required)**

Before running `git commit` and `git push`, you MUST complete this checklist:

#### **1. Markdownlint Compliance** ⚠️ **MANDATORY**
```bash
# Check for violations
markdownlint **/*.md

# Fix critical violations immediately:
# MD047: Files must end with single newline
# MD009: No trailing spaces
# MD026: No trailing punctuation in headings
# MD034: No bare URLs (wrap in <url>)
```

#### **2. File Cleanup** ⚠️ **MANDATORY**
```bash
# Remove ALL non-.md files (scripts, temporary files, etc.)
rm -f *.sh *.py *.js *.json *.txt *.log *.bak *.tmp

# Verify only .md files remain
find . -type f ! -name "*.md" ! -path "./.git/*" ! -name ".gitignore" ! -name "COMMIT-RULES.md" ! -name "MARKDOWNLINT-PROCEDURE.md"
```

#### **3. Content Validation** ⚠️ **MANDATORY**
- ✅ All agent files contain mandatory logging sections
- ✅ No sensitive information (passwords, keys, tokens) in any file
- ✅ All changes are documented and intentional
- ✅ No placeholder or incomplete content

#### **4. Git Status Verification** ⚠️ **MANDATORY**
```bash
# Verify clean working tree
git status

# All changes should be intentional and documented
git diff --staged
```

## **📝 Commit Message Standards**

### **Required Format:**
```
<TYPE>: <Brief Description>

<Detailed explanation of changes>

### **<Category> Changes:**
- Specific change 1
- Specific change 2

### **Files Modified:**
- file1.md: Description of changes
- file2.md: Description of changes

### **Quality Assurance:**
✅ Markdownlint compliance verified
✅ Non-.md files removed
✅ Mandatory logging sections present
✅ No sensitive information included

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### **Commit Types:**
- **FEAT**: New agent features or capabilities
- **FIX**: Bug fixes or corrections
- **DOCS**: Documentation updates
- **STYLE**: Formatting, markdown fixes
- **REFACTOR**: Code/structure improvements
- **UPDATE**: Content updates, logging additions
- **COMPLIANCE**: Regulatory/compliance changes

## **🔒 Security & Compliance Rules**

### **NEVER Commit:**
- **Scripts**: `*.sh`, `*.py`, `*.js`, `*.json`
- **Temporary Files**: `*.tmp`, `*.bak`, `*.log`
- **Sensitive Data**: API keys, passwords, tokens
- **Build Artifacts**: Compiled files, caches
- **IDE Files**: `.vscode/`, `.idea/`, `*.swp`

### **ALWAYS Include:**
- **Mandatory Logging**: All agents must have logging sections
- **Proper Documentation**: Complete and accurate descriptions
- **Quality Verification**: Markdownlint compliance confirmed
- **Change Tracking**: Clear explanation of what and why

## **🚦 Pre-Push Validation**

### **Final Checklist Before Push:**
```bash
# 1. Final markdownlint check
markdownlint **/*.md && echo "✅ Markdownlint passed" || echo "❌ Fix violations first"

# 2. Verify no unwanted files
find . -name "*.sh" -o -name "*.py" -o -name "*.bak" | head -5 && echo "❌ Remove script files" || echo "✅ No script files"

# 3. Check git status is clean
git status --porcelain | grep -q . && echo "❌ Uncommitted changes exist" || echo "✅ Working tree clean"

# 4. Verify upstream is correct
git remote -v | grep "mdastpak/agents"

# 5. Push to correct branch
git push origin HEAD:v1-crypto-exchange-agents
```

## **⚡ Quick Fix Commands**

### **Emergency Markdownlint Fixes:**
```bash
# Fix MD047: Add final newlines
find . -name "*.md" -exec sh -c 'test "$(tail -c1 "$1")" && echo "" >> "$1"' _ {} \;

# Fix MD009: Remove trailing spaces
find . -name "*.md" -exec sed -i '' 's/[[:space:]]*$//' {} \;

# Fix MD026: Remove heading punctuation
find . -name "*.md" -exec sed -i '' -E 's/^(#+[[:space:]]+.*[^[:space:]])[.!?:;]+[[:space:]]*$/\1/' {} \;
```

### **File Cleanup:**
```bash
# Remove all non-.md files (except git and allowed docs)
find . -type f ! -name "*.md" ! -path "./.git/*" ! -name ".gitignore" ! -name "COMMIT-RULES.md" ! -name "MARKDOWNLINT-PROCEDURE.md" -delete
```

## **🎯 Quality Gates**

### **Automated Checks (Future CI/CD):**
```yaml
pre-commit:
  - markdownlint --config .markdownlint.json **/*.md
  - find . -name "*.sh" -o -name "*.py" | wc -l | grep -q "^0$"
  - grep -r "password\|secret\|key" --include="*.md" . || true
```

### **Manual Verification:**
1. **Content Quality**: All agent files complete and accurate
2. **Documentation Standards**: Consistent formatting and structure
3. **Logging Compliance**: All agents have mandatory logging sections
4. **Security Review**: No sensitive information exposed

## **📚 Reference Documentation**

### **Related Files:**
- `MARKDOWNLINT-PROCEDURE.md` - Detailed markdownlint procedures
- `.gitignore` - Comprehensive file exclusion rules
- `README.md` - Project overview with commit rule reference
- `roadmap.md` - Development roadmap with compliance tracking

### **Key Standards:**
- **Markdown**: CommonMark specification with markdownlint rules
- **Logging**: Mandatory JSON-structured logging for all agents
- **Security**: Zero tolerance for sensitive information exposure
- **Quality**: Enterprise-grade documentation standards

## **🚨 Violation Consequences**

### **Commit Rejection Scenarios:**
- ❌ **Markdownlint violations** - Must be fixed before commit
- ❌ **Script files present** - Remove all non-.md files
- ❌ **Missing logging sections** - Add to all agents
- ❌ **Sensitive information** - Remove immediately
- ❌ **Malformed commit message** - Follow required format

### **Emergency Procedures:**
If you accidentally commit violations:
1. **Immediate Revert**: `git revert HEAD`
2. **Fix Issues**: Apply all mandatory rules
3. **Recommit**: With proper compliance
4. **Force Push**: Only if absolutely necessary

## **✅ Success Criteria**

A commit is successful when:
- ✅ **Zero markdownlint violations** for critical rules
- ✅ **Only .md files** (plus allowed docs) in repository
- ✅ **Complete logging sections** in all agent files
- ✅ **Proper commit message** following required format
- ✅ **No sensitive information** anywhere in codebase
- ✅ **Quality verification** completed and documented

## **📞 Support & Escalation**

If you encounter issues:
1. **Review**: MARKDOWNLINT-PROCEDURE.md for detailed fixes
2. **Automate**: Use quick fix commands above
3. **Verify**: Run complete checklist before retry
4. **Escalate**: Contact repository maintainer if blocked

---

**Remember: These rules ensure the highest quality, security, and compliance standards for our enterprise-grade crypto exchange agent documentation. No compromises allowed! 🔒**
