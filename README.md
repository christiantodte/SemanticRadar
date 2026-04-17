# Fabric Semantic Radar

Semantic governance tooling for Microsoft Fabric that helps teams detect duplicate data sources, overlapping semantic models, and ownership gaps across workspaces and capacities.

The project is notebook-first and designed for practical governance reviews inside Fabric. It scans semantic models, normalizes datasource metadata, identifies consolidation opportunities, and turns the results into action-focused outputs such as executive summaries, action plans, diagnostics, and email drafts.

## Why this exists

As Fabric estates grow, teams often create many semantic models that reuse the same source data, repeat the same business logic, or drift apart across workspaces. That creates:

- semantic model sprawl
- duplicated refresh and maintenance effort
- inconsistent metrics and business definitions
- unclear ownership

Fabric Semantic Radar helps surface those issues quickly so teams can consolidate where it makes sense and intentionally document where duplication is expected.

## What it does

- Discovers semantic models across Fabric workspaces and capacities
- Supports service principal or current-user execution
- Detects duplicate datasource usage through normalized datasource fingerprints
- Identifies likely overlapping semantic models using metadata similarity
- Maps dataset owners and workspace admins to impacted models
- Produces compact, notebook-friendly governance outputs
- Generates email drafts for follow-up with owners and admins
- Supports exclusions for intentional duplicates and sandbox/test scenarios
- Reduces noise by suppressing likely deployment-clone patterns

## Output

The analyzer produces a structured result set and visual notebook output including:

- run diagnostics
- executive summary
- action plan
- responsibility view
- duplicate-source consolidation candidates
- source replacement candidates
- probable duplicate semantic-model candidates
- email drafts for stakeholder follow-up

## Quick Start In Fabric

### Option 1: All-in-one notebook

1. Import 2026_SemanticLink_ChristianTodte_SemanticRadar.ipynb into desired workspace
2. Populate the config cell with required values
5. Run the notebook.

## Authentication Modes

The notebook supports multiple execution patterns:

- `service_principal_capacity`
  Best for broad, capacity-wide governance scans with approved admin access.
- `current_user_capacity_admin`
  Tries admin APIs with the signed-in user, then falls back where needed.
- `current_user_workspace_admin`
  Scans only the workspaces the signed-in user can access, optionally scoped to selected workspaces.

Service principal settings are read from environment variables:

- `FABRIC_GOVERNANCE_TENANT_ID`
- `FABRIC_GOVERNANCE_CLIENT_ID`
- `FABRIC_GOVERNANCE_CLIENT_SECRET`

No secrets should be hardcoded into the notebook.

## Key Configuration Options

- `RUN_PRESET`
- `CAPACITY_NAME`
- `INCLUDE_SEMPY_METADATA`
- `DUPLICATE_THRESHOLD`
- `PROBABLE_DUPLICATE_SIMILARITY_THRESHOLD`
- `VISUALS_ONLY`
- `SHOW_ONLY_ACTIONABLE`
- `ACTION_PLAN_MAX_ROWS`
- `EXCLUDED_SEMANTIC_MODEL_IDS`
- `EXCLUDED_SEMANTIC_MODEL_NAMES`
- `EXCLUDED_WORKSPACE_NAMES`
- `EXCLUDED_MODEL_WORKSPACE_PAIRS`

## Requirements

Python package dependencies:

- `msal`
- `requests`

Optional Fabric runtime enrichment:

- `semantic-link` / `sempy`

## Typical Use Cases

- Identify duplicated semantic models pulling from the same warehouse or database
- Find report-specific models that should be replaced with a shared semantic layer
- Review workspace-by-workspace semantic model sprawl
- Support semantic model rationalization initiatives
- Generate governance review packs for platform or BI teams

## Publishing Notes

Before publishing notebooks to GitHub:

- clear notebook outputs
- keep secrets in environment variables or Key Vault
- review saved metadata and runtime outputs

## Roadmap Ideas

- export findings to a lakehouse or warehouse table
- track governance findings over time
- add richer similarity scoring and suppression rules
- add HTML report export
- add domain-level scorecards

