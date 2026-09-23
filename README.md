# Grandale Place beta testing

Static publishing repository for beta features of the [Grandale Place Community Website](https://grandaleplace.com/).
Only `site/` is published. The license, editor settings, and workflow are not web content.

## Branches

- `main`: the single-page fallback stating that testing is closed.
- `dev`: generated beta output. Do not hand-edit generated files in `site/` here.


## Choose what is live

After the reviewed workflow exists on the default branch, configure Settings → Pages →
Source to **GitHub Actions** when ready. In Actions → **Publish selected beta site** →
**Run workflow**, run the workflow from `main`, choosing `main` (fallback) or `dev` (testing)
in its **source** input. This is manual-only: pushing either branch does not publish.
The environment must permit workflow runs from `main`. The last successful publication
remains live until another succeeds. Choose `main` again to close testing.

Expected URL: https://grandaleplace.github.io/website-beta-testing/ . No custom domain or DNS
change is included. See [GitHub's custom Pages workflow documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).

Beta pages are publicly reachable unless separate hosting access restrictions are configured.
Invitations and the acknowledgment notice do not enforce access control. Never publish resident
or confidential data. The disclaimer is proposed editorial wording, not a guarantee of legal
protection; have HOA counsel approve it before relying on it for that purpose.
