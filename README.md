# Jonathan's Space Archive Mirror

Daily automated mirror of [Jonathan McDowell's General Catalog of Artificial Space Objects (GCAT)](https://planet4589.org/space/gcat/).

## Datasets


Source directories:
- https://planet4589.org/space/gcat/tsv/derived/
- https://planet4589.org/space/gcat/tsv/cat/

| File | Description | Source |
|------|-------------|--------|
| `launchlog.tsv` | Master orbital launch log (1957–present) | [derived/launchlog.tsv](https://planet4589.org/space/gcat/tsv/derived/launchlog.tsv) |
| `active.tsv` | Currently active satellites | [derived/active.tsv](https://planet4589.org/space/gcat/tsv/derived/active.tsv) |
| `satcat.tsv` | Full satellite catalog (all time) | [cat/satcat.tsv](https://planet4589.org/space/gcat/tsv/cat/satcat.tsv) |
| `currentcat.tsv` | All objects currently in orbit (incl. debris) | [derived/currentcat.tsv](https://planet4589.org/space/gcat/tsv/derived/currentcat.tsv) |
| `geotab.tsv` | Geostationary satellite log | [derived/geotab.tsv](https://planet4589.org/space/gcat/tsv/derived/geotab.tsv) |
| `psatcat.tsv` | Payload satellite catalog | [cat/psatcat.tsv](https://planet4589.org/space/gcat/tsv/cat/psatcat.tsv) |
| `ftocat.tsv` | Failed-to-orbit catalog | [cat/ftocat.tsv](https://planet4589.org/space/gcat/tsv/cat/ftocat.tsv) |
| `deepcat.tsv` | Deep space catalog | [cat/deepcat.tsv](https://planet4589.org/space/gcat/tsv/cat/deepcat.tsv) |

## Update Schedule

A GitHub Actions workflow fetches fresh data daily at 6:00 AM EDT. Only commits when files actually change.

## Why Archive?

Jonathan McDowell's GCAT is the most comprehensive public catalog of artificial space objects, maintained by a single researcher at the Harvard-Smithsonian Center for Astrophysics. The datasets are updated in-place — when new data is published, the previous version is overwritten with no public version history.

This archive preserves daily snapshots via automated Git commits, enabling:

- **Temporal analysis** — track how constellations grow, satellites deorbit, and debris accumulates over time by diffing snapshots
- **Reproducible research** — pin analyses to a specific date's data rather than a moving target
- **Resilience** — if the source goes offline or restructures, the historical record is preserved
- **Change detection** — Git diffs reveal exactly what changed: new launches, deorbited satellites, catalog corrections

## Usage

### View data from a specific date

```bash
# List all archive snapshots
git log --oneline

# Check out data as it was on a specific date
git log --before="2026-04-01" -1 --format="%H"   # find the commit
git checkout <commit-hash> -- data/                 # restore that snapshot

# Or in one step — get the last snapshot before a date
git checkout $(git log --before="2026-04-01" -1 --format="%H") -- data/

# Return to latest
git checkout main -- data/
```

### Compare changes between two dates

```bash
# Find commits for two dates
OLDER=$(git log --before="2026-04-01" -1 --format="%H")
NEWER=$(git log --before="2026-05-01" -1 --format="%H")

# Summary of what changed
git diff --stat $OLDER $NEWER -- data/

# Full diff for a specific file (e.g. new satellites added)
git diff $OLDER $NEWER -- data/active.tsv

# Count lines added/removed (≈ objects added/removed)
git diff --numstat $OLDER $NEWER -- data/active.tsv
```

### Quick examples

```bash
# How many active satellites were added last month?
git diff --stat $OLDER $NEWER -- data/active.tsv

# What launches happened between two snapshots?
diff <(git show $OLDER:data/launchlog.tsv) <(git show $NEWER:data/launchlog.tsv)

# Export a historical snapshot to a folder
git archive $OLDER -- data/ | tar -x -C /tmp/gcat-snapshot/
```

## License

> Data on this page are licensed CC-BY. You are free to reuse them but please credit "Jonathan McDowell, https://planet4589.org" or similar.

