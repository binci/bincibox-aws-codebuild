# Binci Box: AWS CodeBuild
Docker image to run [Binci](https://github.com/binci/binci) on top of AWS CodeBuild.

## Usage

### Project setup in the CodeBuild console
Set up a CodeBuild project with a custom container, and specify this one. Under "Advanced", check the "Privileged" checkbox.

### Writing buildspec.yml
In the root of your repo, create a file named `buildspec.yml` and populate it with the following (edit where necessary):

```yaml
#
# To be run on binci/aws-codebuild
#
version: 0.2

phases:
  pre_build:
    commands:
      - dockerd_start
  build:
    commands:
      - binci test
```

When you choose to run builds on a custom container, AWS ignores the Docker `ENTRYPOINT`, which Amazon uses to start the docker daemon in their own containers. Therefore, the `dockerd_start` command in the `pre_build` path above is necessary to make sure Docker is running before starting Binci.

## License
All content in this repository is openly licensed under the MIT license unless otherwise noted. Original content is Copyright 2017 by the Binci Team.

