# Grandale Place beta testing

Static publishing repository for [Grandale Place](https://grandaleplace.com/).
Website source and beta build/export tooling live in the separate `hoa` repository.
Only `site/` is published. The license, editor settings, and workflow are not web content.

## Branches

- `main`: the single-page fallback stating that testing is closed.
- `dev`: generated beta output. Do not hand-edit generated files in `site/` here.
- `feature/codex/*`: reviewable repository changes before they are adopted.

Initialize `main` with the reviewed fallback setup, then create `dev` from it. Keep the
workflow and repository tooling on both branches. Exporting updates only `site/`.
Do not merge generated `dev` content into `main`; that would replace the fallback.

## Export active testing

With a clean `dev` checkout here, run from `hoa` using Node.js 26:

```sh
npm run export:beta -- ../beta-hoa
```

This builds fresh beta output for the root of any hostname, removes the production CNAME,
adds noindex directives, and replaces only `site/`. Review, commit and push `dev` separately.
No export command pushes, changes Pages settings, or deploys.

## Choose what is live

After the reviewed workflow exists on the default branch, configure Settings → Pages →
Source to **GitHub Actions** when ready. In Actions → **Publish selected beta site** →
**Run workflow**, run the workflow from `main`, choosing `main` (fallback) or `dev` (testing)
in its **source** input. This is manual-only: pushing either branch does not publish.
The environment must permit workflow runs from `main`. The last successful publication
remains live until another succeeds. Choose `main` again to close testing.

The webmaster manages the beta DNS hostname. Exports use domain-independent root paths and
omit hostname-specific canonical metadata by default, so changing the hostname requires no
rebuild. Do not add a `/website-beta-testing` prefix when serving at a custom-domain root.
Only subfolder hosting needs `BETA_BASE_PATH`; see `hoa/docs/beta.md`. The export does not
change DNS or Pages settings. See [GitHub's custom Pages workflow documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).

Beta pages are publicly reachable unless separate hosting access restrictions are configured.
Invitations and the acknowledgment notice do not enforce access control. Never publish resident
or confidential data. The disclaimer is proposed editorial wording, not a guarantee of legal
protection; have HOA counsel approve it before relying on it for that purpose.

## Local previews

From the sibling `hoa` source repository, run `make preview-beta` and open
http://localhost:8081 . It builds the current source with the beta banners and acknowledgment
screen. Stop it with `make down-beta`. The normal `make preview` uses port 8080.

To preview this repository's exported files or fallback directly, use Python 3.14
(or the VS Code **Preview site** task):

```sh
python3.14 -m http.server 8082 --bind 127.0.0.1 --directory site
```

Open http://127.0.0.1:8082 . Root-path exports work here without rewriting any links.
No Node dependencies or build step are required in this publishing repository.
