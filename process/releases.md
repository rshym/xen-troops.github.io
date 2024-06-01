# Requirements for releases

Each repo has its release schedule. Release may be created for different
reasons, like:
- obligations before the customer
- significant change in the API provided by the project
- the need to change the build base, like upgrade the yocto version
- the periodic milestone of the actively developing project
- ...

Despite the reasons, the release has the following requirements:
- all external dependencies have to be fixed using the commit hash or
release tag only
- the usage of the developer's forks of the xen-troops' repos is not acceptable
- the head of the branch of the external repo can't be used in the release

To be more specific:
- for yocto recipes, if SRC_URI has any internet link, there has to be SRCREV
with the commit hash or release tag (AUTOREV can't be used)
- any component mentioned in the `sources:` block of the moulin configuration
(.yaml) has to have `rev:` set to the commit hash or release tag (branch name
can't be used)
- android manifest has to have fixed commits

Before the release, we need to take into account the impact on other dependable
repos. This means, that release notes have to describe:
- changes in the provided API
- changes in build requirements
- expected build issues and possible solutions
- known issues with workaround

## Release branches
We make the release from the main branch of our repo in most cases.
Only in some rare cases, we release from the already existing
platform-specific branch. But this need should be seriously considered
and require management review & approval.

For the release, we should create the release branch `vX.Y` from the main
branch. So, for the release `2.3.0` we use branch `v2.3`.
All hotfixes for that release have to be added to the same release branch
with the new release tag.
For example, hotfix was made for the release `2.3.0`. It must be pushed
into the branch `v2.3`, and have to be tagged as `v2.3.1`.
