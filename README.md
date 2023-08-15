# Common CI workflows for OpenConfig Projects

## Standard Usage

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
    uses: openconfig/common-ci/.github/workflows/go.yml@v1.0.0

  linter:
    uses: openconfig/common-ci/.github/workflows/linter.yml@v1.0.0
```

Then copy the sample linter configurations folder into your repository:

```bash
cp -r common-ci/.github/linters YOUR-REPO/.github/linters
```

At this point, you may wish to change the configuration of these linters to suit
your own repository.

## Basic Usage

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
    uses: openconfig/common-ci/.github/workflows/basic_go.yml@v1.0.0
```

## Flags

Some flags are supported for customizing the CI workflow, for example,

```yaml
jobs:
  go:
    uses: openconfig/common-ci/.github/workflows/basic_go.yml@v1.0.0
    with:
      static-analysis-excludes-regex: exampleoc
      skip-gofmt: true
      skip-staticcheck: true
```

For all supported flags, see the corresponding reusable workflow definitions
under [.github/workflows](.github/workflows).
