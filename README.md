# macOS M1 Preview Documentation

The purpose of this repository is to walk you through the details of the macOS M1 preview on CircleCI.

## What are macOS M1 resources on CircleCI?

The M1 resource class is a new macOS option, running on Apple Silicon hardware, for those developing, building, testing, and signing iOS, iPadOS, macOS, WatchOS, and tvOS applications using the Xcode IDE.

### Supported Xcode Images
* [Xcode 14.0.1](https://circleci.com/docs/testing-ios#supported-xcode-versions)
* [Xcode 13.4.1](https://circleci.com/docs/testing-ios#supported-xcode-versions)
### Known Limitations
* A security review of the new platform is underway.
* Not compatible with macOS orb.
* SIP is enabled; file system modification commands will fail.
## Pricing and Specs
The following macOS M1 resource class is available:

|Resource Class Name|vCPU|Memory|Cost
|---|---|---|---|
|`macos.m1.medium.gen1`|4|8 GB|TBD credits per minute

## Example of a CircleCI config using macOS M1 resources
```yaml
# .circleci/config.yml
version: 2.1
jobs: # a basic unit of work in a run
  build-and-test: # your job name
    macos:
      xcode: 13.4.1 # indicate your selected version of Xcode
    resource_class: macos.m1.medium.gen1
    steps: # a series of commands to run
      - checkout  # pull down code from your VCS
      - run: bundle install
      - run:
          name: Fastlane
          command: bundle exec fastlane $FASTLANE_LANE
      - store_artifacts:
          path: output
      - store_test_results:
          path: output/scan
          
workflows:
  build-test:
    jobs:
      - build-and-test
```
## How to provide feedback & frequently asked questions
Please [open an issue](https://github.com/CircleCI-Public/macos-dedicated-host-preview-docs/issues) with any feedback or to report any issues that you encounter.
### FAQ
* Can I run end-to-end tests on M1 resources? (being verified)
  * Yes! Our M1 resource class provide access to the GPU, allowing for full E2E testing that was previously [unavailable](https://support.circleci.com/hc/en-us/articles/360052160592-Tests-Fail-With-Error-There-is-no-available-Metal-device-on-this-system-) on macOS VMs.
