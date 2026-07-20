# NaMarrado ECA development workflow

This fork keeps two kinds of history separate:

- `master` mirrors the original project's `upstream/master`.
- `nam-ver` is the long-lived NaMarrado build with private visual and functional customizations.

## Keep `nam-ver` compatible with upstream

Periodically merge the original project into the custom branch:

```sh
git switch nam-ver
git fetch upstream
git merge upstream/master
git push origin nam-ver
```

Do not merge the whole `nam-ver` branch into `master`. Git `rerere` is enabled
locally so resolutions of recurring merge conflicts can be reused.

## Contribute only selected changes upstream

Keep each logical change in its own commit. For a change that should become a
real upstream pull request, create a clean contribution branch from upstream and
copy only the chosen commits:

```sh
git fetch upstream
git switch -c contrib/<change-name> upstream/master
git cherry-pick -x <chosen-commit>
git push -u origin contrib/<change-name>
```

Open the pull request from `contrib/<change-name>` to the original project's
`master`. Custom visual or product-specific commits remain only in `nam-ver`.

## Refresh the fork's clean base branch

```sh
git switch master
git fetch upstream
git merge --ff-only upstream/master
git push origin master
git switch nam-ver
```
