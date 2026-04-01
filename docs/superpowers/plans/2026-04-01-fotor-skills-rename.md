# Fotor Skills Rename Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rename the bundled skill from `test-openapi` to `fotor-skills`, move it to `skills/fotor-skills/`, and update all repository URLs to the organization-owned GitHub repository.

**Architecture:** This change is a repository-wide rename with no intended behavioral change. The safest path is to codify the expected end state in a small regression test, perform the directory and text migration, then verify there are no stale names or URLs left in the tree.

**Tech Stack:** Markdown, YAML, Python standard library (`unittest`), Git

---

### Task 1: Add rename regression coverage

**Files:**
- Create: `tests/test_skill_rename.py`

- [ ] **Step 1: Write the failing test**

```python
def test_skill_directory_and_identifiers_are_renamed():
    ...
```

- [ ] **Step 2: Run test to verify it fails**

Run: `python3 -m unittest tests.test_skill_rename -v`
Expected: FAIL because `skills/fotor-skills/` and the new names/URLs do not exist yet

- [ ] **Step 3: Write minimal implementation**

Perform the repository rename so the assertions become true.

- [ ] **Step 4: Run test to verify it passes**

Run: `python3 -m unittest tests.test_skill_rename -v`
Expected: PASS

### Task 2: Rename the skill and update repository references

**Files:**
- Modify: `README.md`
- Modify: `CHANGELOG.md`
- Modify: `skills/fotor-skills/SKILL.md`
- Modify: `skills/fotor-skills/agents/openai.yaml`
- Modify: `skills/fotor-skills/references/install-or-upgrade.md`
- Modify: `skills/fotor-skills/scripts/check_skill_update.py`
- Rename: `skills/test-openapi/` -> `skills/fotor-skills/`

- [ ] **Step 1: Rename the directory**

Run: `mv skills/test-openapi skills/fotor-skills`

- [ ] **Step 2: Update user-facing names and paths**

Replace `test-openapi` path/name references with `fotor-skills`.

- [ ] **Step 3: Update repository URL references**

Replace `https://github.com/zeng121/skill-beta.git` and `zeng121/skill-beta` with `https://github.com/fotor-ai/fotor-skills.git` and `fotor-ai/fotor-skills`.

### Task 3: Verify no stale references remain

**Files:**
- Test: `tests/test_skill_rename.py`

- [ ] **Step 1: Run the regression test**

Run: `python3 -m unittest tests.test_skill_rename -v`
Expected: PASS

- [ ] **Step 2: Run repository-wide stale-reference searches**

Run: `rg -n "test-openapi|zeng121/skill-beta|github.com/zeng121/fotor-skills|github.com/zeng121/skill-beta" -S .`
Expected: no matches
