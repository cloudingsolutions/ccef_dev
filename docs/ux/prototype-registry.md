# Prototype Registry

This registry records external UX/UI prototype revisions that product artifacts and downstream work items may use as visual and interaction references.

Prototype repositories can continue to evolve. Product slices, change requests, milestones, tasks, and work items must reference a pinned prototype revision when they depend on a prototype-defined screen or state.

## Usage Rules

- Reference prototype revisions by repository, path, and full commit SHA.
- Do not rely on a moving branch name as implementation input.
- For prototype-defined screens and states, downstream agents must inspect the pinned revision and preserve its look and feel.
- For undefined screens and states, downstream agents may extrapolate only within the pinned prototype's established design language.
- A newer prototype commit does not automatically change approved product scope. It must be reviewed as refinement input, a change request, or future-slice input.
- If a referenced prototype revision cannot be accessed, prototype-defined UI work should block rather than invent a replacement look and feel.

## Safe Agent Access Pattern

Agents should inspect pinned prototype revisions without disturbing the active UX repository checkout.

Preferred read-only inspection:

```bash
git -C /Users/wolney/repos/projects/ccef-ui-ux show <commit>:prototype/index.html
```

Preferred browser/manual inspection:

```bash
git -C /Users/wolney/repos/projects/ccef-ui-ux worktree add /tmp/ccef-ui-ux-<short-commit> <commit>
```

Then inspect:

```text
/tmp/ccef-ui-ux-<short-commit>/prototype/index.html
```

Do not run `git checkout <commit>` in `/Users/wolney/repos/projects/ccef-ui-ux` unless the repository is clean and the task explicitly allows moving that working copy.

## Registered Prototype Revisions

| Prototype Revision ID | Product/Slice Usage | Repository | Source Path | Commit | Branch At Capture | Captured At | Repo State At Capture | Notes |
|---|---|---|---|---|---|---|---|---|
| UXPROTO-CCEF-001 | Visual authority for PS-CCEF-001 prototype-defined screens and states | `/Users/wolney/repos/projects/ccef-ui-ux` | `prototype/index.html` | `042b05cfa0c9664eb542ca922ba69be537ec5ad2` | `main` | 2026-07-21 | Clean | Commit subject: `Merge pull request #2 from cloudingsolutions/design/slice-2-wizard`; file blob `5f34d27603c2b438a903f9b05f6eaa5f4b18d435` |

## Change Handling

When a newer UX prototype commit should influence product work:

1. Add or update a registry row for the new pinned revision.
2. Compare the old and new prototype revisions.
3. Classify changes as one of:
   - current-slice clarification;
   - current-slice change request;
   - future-slice candidate;
   - visual-only improvement;
   - rejected/no product impact.
4. Update the relevant UX reference or traceability documents.
5. Update canonical slice, use case, requirement, ADR, milestone, task, or work item artifacts only after the change is accepted.
