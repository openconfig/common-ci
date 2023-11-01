# Common CI workflows for OpenConfig Projects

## Upgrading CI Version

### Automatically Updating CI Version

GitHub's dependabot supports updating reusable workflows.

Here is an example of how to
[enable dependabot](https://github.com/openconfig/goyang/pull/253/files), and
what an [update PR](https://github.com/openconfig/goyang/pull/254) looks like.

### Manually Updating CI Version

When updating a repository to use the latest reusable CI workflow on the main
branch, `<latest SHA>` should be used following the safest security and
stability recommendations:
[Stability Recommendations](https://docs.github.com/en/actions/using-workflows/reusing-workflows#calling-a-reusable-workflow)

Do this by simply updating the SHA in the user repository's
`.github/workflows/go.yml` to the SHA of the current main branch
([example](https://github.com/openconfig/kne/pull/371/files#diff-678682767f2477de3e3c546746f8568b9a1942b2c647d32331d7e774b8ff8d9f)).
If you created a PR to update the reusable workflow, then this will be available
after the PR is merged.

## First-time Use

### Standard Go Usage

Copy the following into your repository's `.github/workflows/go.yml`:

```yaml
name: Go

on:
  push:
    branches: [ master ]
  pull_request:
  schedule:
    - cron: "0 0 * * *"

jobs:
  go:
    uses: openconfig/common-ci/.github/workflows/go.yml@<latest SHA>

  linter:
    uses: openconfig/common-ci/.github/workflows/linter.yml@<latest SHA>
```

Then copy the sample linter configurations folder into your repository:

```bash
cp -r common-ci/.github/linters YOUR-REPO/.github/linters
```

At this point, you may wish to change the configuration of these linters to suit
your own repository.

### Basic Go Usage (for simple Go repositories)

If you do not want to maintain linter configuration, then you may use the basic
workflow, which only involves copying the following into your repository's
`.github/workflows/go.yml`:

```yaml
name: Go

on:
  push:
    branches: [ master ]
  pull_request:
  schedule:
    - cron: "0 0 * * *"

jobs:
  go:
    uses: openconfig/common-ci/.github/workflows/basic_go.yml@<latest SHA>
```

### Flags

Some flags are supported for customizing the CI workflow, for example,

```yaml
jobs:
  go:
    uses: openconfig/common-ci/.github/workflows/basic_go.yml@<latest SHA>
    with:
      static-analysis-excludes-regex: exampleoc
      skip-gofmt: true
      skip-staticcheck: true
```

For all supported flags, see the corresponding reusable workflow definitions
under [.github/workflows](.github/workflows).
