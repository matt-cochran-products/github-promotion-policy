# Proposed Zonetico promotion build gate

Scope: matt-cochran-products/zonetico-saas repository ruleset 24804360 only.

Squash-only dev merges discard staging ancestry even when a feature branch reconciles it. Strict ancestry synchronization therefore conflicts with merge-commit promotion through dev → staging → main.

Change only strict_required_status_checks_policy from true to false. Keep Build gate required from GitHub Actions integration 15368 on staging and main. Organization review, source-branch workflow, merge methods, deletion and force-push protections remain enforced separately. Promotion CI uses the default pull-request checkout, testing GitHub's generated merge commit; Rust and TypeScript must pass. All eight exact-image acceptance checks still precede restricted production promotion.

Tradeoff: source ancestry synchronization is no longer required when the target changes. Reviewers must ensure merge-result CI remains current after target changes and rerun it where necessary. Failed or outdated validation must not be merged.

Review and merge this proposal before application. Fetch the current ruleset and verify it matches this payload except for the strict flag. Stop if any other field changed. Apply only to the named repository and ruleset, read it back, and verify effective staging and main branch rules. This proposal applies nothing automatically and changes no organization ruleset.

The overdue P02 Stripe proof is an independent CI failure. This policy change does not make #610 eligible while its build gate fails.
