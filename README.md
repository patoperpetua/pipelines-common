# SINGLETON SD - PIPELINES - COMMON

This project contains common gitlab-ci templates.

> The **main repository** is hosted in [gitlab.com/singletonsd/pipelines/common](https://gitlab.com/singletonsd/pipelines/common.git) but it is automaticaly mirrored to [github.com/singletonsd](https://github.com/singletonsd/pipelines-common.git), [github.com/patoperpetua](https://github.com/patoperpetua/pipelines-common.git) and to [gitlab.com/patoperpetua](https://gitlab.com/patoperpetua/pipelines-common.git). If you are in the Github page it may occur that is not updated to the last version.

## AVAILABLE FILES

There are 3 files:

- **pages:** contains a job to publish files into gitlab pages. There is 1 job:
  - **pages:** copy the contents of a source folder to a target folder. It has the following available variables:
    - *PAGES_TARGET_FOLDER:* "public"
    - *PAGES_SOURCE_FOLDER:* "dist"

- **scripts:** contains jobs to test bash scripts and publish them to gitlab pages as single file and inside a zip file. It has the following available variables:
  - *SCRIPTS_SKIP_TEST*: ""
  - *SCRIPTS_SKIP_ZIP*: ""

- **templates:** contains jobs to test gitlab-ci templates and publish them to gitlab pages.

## HOW TO

### USE

If you want to skip reading, you can copy and paste one of the following links and setup the variables:

- [Pages](https://gitlab.com/singletonsd/pipelines/common/raw/master/examples/.gitlab-ci-example-pages.yml)
- [Scripts](https://gitlab.com/singletonsd/pipelines/common/raw/master/examples/.gitlab-ci-example-scripts.yml)
- [Templates](https://gitlab.com/singletonsd/pipelines/common/raw/master/examples/.gitlab-ci-example-templates.yml)

To use it, you can include them as following (using repository aproach):

```yaml
include:

  - project: 'singletonsd/pipelines/common'
    file: '/src/.gitlab-ci-pages.yml'
  - project: 'singletonsd/pipelines/common'
    file: '/src/.gitlab-ci-test-scripts.yml'
  - project: 'singletonsd/pipelines/common'
    file: '/src/.gitlab-ci-templates.yml'
```

Or using remote approach over gitlab repo:

```yaml
include:
  - remote: 'https://gitlab.com/singletonsd/pipelines/common/raw/master/src/.gitlab-ci-pages.yml'
  - remote: 'https://gitlab.com/singletonsd/pipelines/common/raw/master/src/.gitlab-ci-scripts.yml'
  - remote: 'https://gitlab.com/singletonsd/pipelines/common/raw/master/src/.gitlab-ci-test-templates.yml'
```

Or using remote approach over gilab pages:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/common/latest/.gitlab-ci-pages.yml'
  - remote: 'https://singletonsd.gitlab.io/pipelines/common/latest/.gitlab-ci-scripts.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/common/latest/.gitlab-ci-test-templates.yml'
```

Master branch is setup as latest folder. To use an specific version, put the version name before the file name like:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/common/1.0.0/.gitlab-ci-${FILE}.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/common/develop/.gitlab-ci-${FILE}.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/common/feature-new/.gitlab-ci-test-${FILE}.yml'
```

And also define the stages you want to use, like following:

```yaml
# Pages
stages:
  - deploy

# Scripts
stages:
  - test
  - build
  - deploy

# Templates
stages:
  - test
  - deploy
```

### TEST

You can test your .gitlab-ci.yml files by executing the following:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh | bash /dev/stdin
```

That script contains the following options:

```bash
-h | --help: display help.
-o | --only: the name of the file or folder to test.
```

Also you can download the script by:

```bash
curl -o gitlab-ci_lint_test_standalone.sh -L https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh
```

## GIT HOOK

You can setup gitlab lint tester to be run before a commit. To do that just execute the following script under your git repository:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_hook_installer.sh | bash /dev/stdin
```

## DOCUMENTATION

- [Gitlab CI - Includes](https://docs.gitlab.com/ee/ci/yaml/)

## TODO

- [X] Add pages template.
- [X] Add script template.
- [X] Add template template.
- [ ] Fix documentation.
- [X] Add examples.

----------------------

© [Singleton SD](http://www.singletonsd.com), Italy, 2019.
