# circleci-commitlint-step

Commit message validation with `commitlint` npm package

## What it does?

![alt text](https://github.com/SecretBase/circleci-commitlint-step/blob/master/.github/circle_fail.png)

![alt text](https://github.com/SecretBase/circleci-commitlint-step/blob/master/.github/circle_success.png)

## Use

Add the following step to your circleci `config.yml`:

```
version: 2

jobs:
  commitlint:
    docker:
      - image: tromantic/circleci-commitlint:latest
    working_directory: /www
    environment:
      CIRCLE_COMPARE_URL: << pipeline.project.git_url >>/compare/<< pipeline.git.base_revision >>..<<pipeline.git.revision>>
    steps:
      - checkout
      - run:
          name: Lint commit messages
          command: |
            /bin/sh /.scripts/commitlint_range.sh

workflows:
  version: 2
  my_pipeline:
    jobs:
      - commitlint
```

## Private repo settings

You will need to have a github OAUTH token to get the pull request details
Create an environment variable in your circleci repository
`GITHUB_TOKEN_COMMITLINT=yourToken`

## References

- [commitlint](https://github.com/marionebl/commitlint)
- [commitizen](https://github.com/commitizen/cz-cli)
