# NICU to Home

A shopping agent for parents of premature and medically complex children in Canada and the US. See README.md for what it does and CONTRIBUTING.md for the content rules.

## How changes ship

- **Maintainer's own changes** (made in a session with the maintainer): run the checks below, then commit and push straight to `main`. No pull request needed.
- **Outside contributions:** always a pull request, reviewed by the maintainer before merge. Branch protection on `main` enforces this for everyone except the maintainer.
- Never force-push `main`.

## Checks before every push

- Issue-form YAML parses: `ruby -ryaml -e 'Dir[".github/ISSUE_TEMPLATE/*.yml"].each { |f| YAML.load_file(f) }'`
- Relative links in Markdown files point to files that exist.
- Once code exists, its tests and linters run here too.

## Content rules that are easy to get wrong

- Suggestions are peer experience, labelled "shared by a parent, not a professional". Hard limits: no doses, nothing that tells a family to stop or change a prescribed treatment, no diagnosing.
- "Check with" wording depends on country: Canadian families have a dietitian; many US families don't.
- Never commit raw group captures (`captures/`), Shopify catalog results (`cache/`), or anything that identifies a family.
- No paid ranking: commission or affiliate data never influences what is shown.
