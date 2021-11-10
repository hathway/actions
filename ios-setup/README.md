# ios-setup

## Info

This action will:

- clone source code
- install Ruby and gems. this is needed for running fastlane. it caches bundler output, that improves performance of that operation
- adds post hook that will delete all the files inside of the work directory, this is needed to free up space on a build node
    Additional configuration adjustments should be done inside of the `Gymfile` for fastlane, to make all the artifacts, related to the build, stored inside of the workspace and not in the system directories

    ```ruby
    build_path('./artifacts/build/')
    archive_path('./artifacts/archive/')
    derived_data_path('./artifacts/der_data/')
    cloned_source_packages_path('./artifacts/spm/')
    ```

## Configuration

This action accepts following parameters:

- `ruby_version`: ruby version to be installed, for example: `3.0.2`
- `macos_image`: this value is used by ruby action to download prebuilt Ruby for the specific macos version, for example: `macos11.1`

## Example

Here is an example of this action usage:

```yml
jobs:
  build:
    runs-on: [ self-hosted, macos ]

    steps:
      - name: Env Setup
        uses: hathway/actions/ios-setup@master
        with:
          ruby_version: 3.0.2
          macos_image: macos11.1
        
      # Fastlane build steps go here

```
