# Upstream Update Guide

This guide explains how to easily update your DeckLock fork with the latest features from upstream, without merge conflicts.

## What Changed

Your repository is now configured to avoid merge conflicts when syncing with upstream:

1. **`.gitignore`** - Ignores `content/`, `docs/` directories (upstream demo content and builds)
2. **`.gitattributes`** - Protects your `mycontent/` from being overwritten during merges
3. **Upstream remote** - Configured to point to https://github.com/4dcu-be/DeckLock.git

## How to Update from Upstream (Simple Method)

When you want to pull in new features from the original DeckLock repository:

```bash
# 1. Fetch the latest changes from upstream
git fetch upstream

# 2. Merge upstream changes into your current branch
git merge upstream/master --no-edit

# 3. Push your updated branch
git push origin main
```

**That's it!** No rebase conflicts, no manual merging needed.

## What This Protects

✅ **Your data** - `mycontent/` is protected by .gitattributes
✅ **No demo conflicts** - `content/` is gitignored, won't cause conflicts
✅ **No build conflicts** - `docs/` is gitignored, won't cause conflicts
✅ **Code updates** - You still get plugin updates, bug fixes, and new features from upstream

## Testing the Merge (Optional)

If you want to test before merging:

```bash
# Create a test branch
git checkout -b test-upstream-merge

# Try the merge
git fetch upstream
git merge upstream/master

# If it looks good:
git checkout main
git merge upstream/master
git push

# If there are issues:
git checkout main
git branch -D test-upstream-merge
```

## What Gets Updated

When you merge from upstream, you'll receive:

- ✅ Plugin improvements (MTG, KeyForge, Gwent, FAB)
- ✅ Theme and styling updates
- ✅ Bug fixes
- ✅ New features
- ✅ Configuration file updates (you may need to manually adjust)

## What Stays Yours

Your custom content is always preserved:

- ✅ All files in `mycontent/`
- ✅ Your cache in `mycontent/dl_cache/`
- ✅ Any custom modifications you've made

## Troubleshooting

### If you get conflicts in configuration files

Upstream might update `pelicanconf.py`, `Makefile`, or `publishconf.py`. If you customized these:

```bash
# After merge conflict, check the conflict
git status

# Edit the conflicting files to keep your customizations
# Then mark as resolved:
git add <file>
git commit
```

### If you accidentally committed to docs/ or content/

These directories are now ignored. If you accidentally committed to them before:

```bash
git rm -r --cached content/data/
git rm -r --cached docs/
git commit -m "Remove accidentally committed files"
```

## Merge vs Rebase

**Before**: You used `git rebase`, which caused conflicts with `content/` and `docs/`
**Now**: You use `git merge`, which is simpler and conflict-free thanks to `.gitignore` and `.gitattributes`

**Why merge is better for forks:**
- Preserves your commit history
- No force-push needed
- Automatic conflict resolution for protected directories
- Easier to understand what changed

---

**Questions?** Check the main [README.md](README.md) or [FORK_GUIDE.md](FORK_GUIDE.md) for more details.
