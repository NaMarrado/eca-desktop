# NaMarrado ECA development workflow

This fork keeps two kinds of history separate:

- `master` stays compatible with `upstream/master` and contains only changes
  deliberately selected for public or upstream use.
- `nam-ver` is the long-lived NaMarrado build with private visual and functional customizations.

## Bring upstream changes into the custom build

Update `master` from the original project, then merge that clean integration
branch into `nam-ver`:

```sh
git switch master
git fetch upstream
git merge upstream/master
git push origin master
git switch nam-ver
git merge master
git push origin nam-ver
```

Do not merge the whole `nam-ver` branch into `master`. Git `rerere` is enabled
locally so resolutions of recurring merge conflicts can be reused.

## Promote only selected changes

Keep each logical change in its own commit. Copy only a chosen commit from
`nam-ver` into `master`:

```sh
git switch master
git fetch upstream
git merge upstream/master
git cherry-pick -x <chosen-commit>
git push origin master
```

Custom visual or product-specific commits remain only in `nam-ver`. When
separate changes need separate pull requests, create `contrib/<change-name>`
from `upstream/master` and cherry-pick only the commits for that one PR.

## Refresh the fork's clean base branch

```sh
git switch master
git fetch upstream
git merge upstream/master
git push origin master
git switch nam-ver
```
