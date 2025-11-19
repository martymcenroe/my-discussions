### Summary

I’d like a way to enable and manage the **“Sponsorships” repo feature** programmatically for multiple repositories – via API and/or GitHub CLI – rather than clicking the checkbox in each repo’s Settings → General → Features.

### Problem

As a maintainer with many repositories, I want a consistent GitOps-style way to control repo features. Today:

- I can configure the funding sources themselves with `.github/FUNDING.yml`.
- I can script repo creation, topics, branch protection, etc., via the REST/GraphQL APIs and `gh` CLI.
- But I cannot enable the **Sponsorships** repo feature (that controls whether the Sponsor button appears) without going into each repo’s Settings page in the UI.

For someone with dozens of public repos, this means a lot of manual clicking just to turn on the same feature everywhere that already has a valid `FUNDING.yml`.

### Proposed solutions

Any of the following would solve the problem:

1. **Expose the Sponsorships feature in the API**, e.g.:
   - A REST/GraphQL field on the repository object (boolean such as `has_sponsorships_feature`).
   - Allowing PATCH/ mutation updates to that field for maintainers with admin rights.

2. **Support it in the GitHub CLI**, for example:
   - `gh repo edit --enable-sponsorships true`
   - or similar.

3. **Optional global default** (nice to have):
   - An account/org-level setting: “Enable Sponsorships for all new public repos that contain a FUNDING.yml”.

### Why this matters

- Maintainers who use infrastructure-as-code for repos expect feature flags to be manageable via API/CLI, not only via UI checkboxes.
- GitHub Sponsors already supports automation on the funding side through `.github/FUNDING.yml`; adding programmatic control of the repo feature flag would make it consistent.
- This change would especially help people who:
  - Maintain many small OSS projects.
  - Move repos between orgs or split/merge repos over time.
  - Want a clean, repeatable setup process for new repos that includes sponsorship.

Thanks for considering this – it would remove a small but persistent bit of friction from using GitHub Sponsors at scale.
