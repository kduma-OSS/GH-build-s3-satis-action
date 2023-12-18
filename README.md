# `s3-satis` build GitHub Action

To ease the process of building and publishing Composer repository to S3 bucket,
in fully serverless manner, this GitHub Action was created.

Check full documentation here: [opensource.duma.sh/systems/serverless-satis/s3-satis-github-action](https://opensource.duma.sh/systems/serverless-satis/s3-satis-github-action)

## Usage

In your workflow file, add following step:

```yaml
name: Main

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Build Satis Repo
        uses: kduma-OSS/GH-build-s3-satis-action@v2
        with:
          s3-access-key-id: ${{ secrets.S3_ACCESS_KEY_ID }}
          s3-secret-access-key: ${{ secrets.S3_SECRET_ACCESS_KEY }}
          s3-region: ${{ vars.S3_REGION }}
          s3-bucket: ${{ vars.S3_BUCKET }}
          s3-endpoint: ${{ vars.S3_ENDPOINT }}
```

## Configuration options

| Option                       | Description                       | Type                                    | Required |    Default    |
|------------------------------|-----------------------------------|-----------------------------------------|:--------:|:-------------:|
| `satis-config-path`          | Path to satis.json file           | `string`                                |    No    | `satis.json`  |
| `s3-satis-version-tag`       | Docker image version tag to use   | `string`                                |    No    |     `v0`      |
| `repository-url`             | URL of repository to update       | `string`                                |    No    |               |
| `verbosity`                  | Verbosity level of satis          | `normal` or `verbose` or `very_verbose` |    No    |   `normal`    |
| `use-cache`                  | Use cache for satis               | `boolean`                               |    No    |    `false`    |
| `fresh`                      | Force satis to rebuild repository | `boolean`                               |    No    |    `false`    |
| `cache-path`                 | Path to cache directory           | `string`                                |    No    | `satis-cache` |
| `s3-access-key-id`           | S3 access key ID                  | `string`                                |   Yes    |               |
| `s3-secret-access-key`       | S3 secret access key              | `string`                                |   Yes    |               |
| `s3-region`                  | S3 region                         | `string`                                |    No    |               |
| `s3-bucket`                  | S3 bucket                         | `string`                                |   Yes    |               |
| `s3-endpoint`                | S3 endpoint                       | `string`                                |    No    |               |
| `s3-use-path-style-endpoint` | S3 use path style endpoint        | `boolean`                               |    No    |    `false`    |

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Build Satis Repo
        uses: kduma-OSS/GH-build-s3-satis-action@v2
        with:
          satis-config-path: satis.json
          s3-satis-version-tag: v0
          repository-url:
          verbosity: normal
          use-cache: false
          fresh: false
          cache-path: satis-cache
          s3-access-key-id: 
          s3-secret-access-key: 
          s3-region: 'us-east-1'
          s3-bucket: 
          s3-endpoint: 
          s3-use-path-style-endpoint: false
```
