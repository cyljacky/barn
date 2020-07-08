# Automation - Gitlab CICD

When using GitLab CI/CD based, sometimes hitting error message:`ERROR: Invalid argument: sh`

which stops the CI/CD, it's because the image used in `.gitlab-ci.yml` has predefined `entrypoint` . We need to overwrite the entrypoint written in the image. `image:entrypoint` [https://docs.gitlab.com/ee/ci/yaml/README.html\#imageentrypoint](https://docs.gitlab.com/ee/ci/yaml/README.html#imageentrypoint) provides user to overwrite the field.

p.s. just fill in `['']` to erase the field should be enough, as the `script` section wrapped the command with `sh` .



