# Examples


## Build without publishing commands
```yaml
description: >
  Build, but don't publish, an image using the check and build jobs.

usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  jobs:
    check_and_build_only:
      executor: kaniko-publish/kaniko
      steps:
        - checkout
        - kaniko-publish/check
        - kaniko-publish/build-and-push:
            deploy: false

  workflows:
    build_without_publishing:
      jobs:
        - check_and_build_only
```


## Build without publishing a job
```yaml
description: >
  Build, but don't publish, an image using the publish job.

usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    build_without_publishing:
      jobs:
        - kaniko-publish/publish:
            deploy: false
            tar_path: container.tar
```

## Caching layers
```yaml
description: Use the Docker Registry to cache built layers
usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    build_and_publish_image:
      jobs:
        - kaniko-publish/publish:
            cache_repo: "myorg/repo"
```

## Custom name and tag
```yaml
description: Build and Deploy image with a custom name and tag.
usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    build_and_publish_image:
      jobs:
        - kaniko-publish/publish:
            image: my/image
            tag: my_tag
```

## Custom registry and dockerfile
```yaml
description: |
  Build and Deploy image with a non standard Dockerfile and to a
  custom registry.
usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    build_and_publish_image:
      jobs:
        - kaniko-publish/publish:
            image: my.docker.registry/image
            dockerfile: path/to/MyDockerFile
```

## Lifecycle hooks
```yaml:examples/life-cycle-hooks.yml
description: |
  Build and deploy an image with custom lifecycle hooks; before
  checking out the code from the VCS repository, before building the
  docker image, and after building the docker image.
usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    workflow_with_lifecycle:
      jobs:
        - kaniko-publish/publish:
            after_checkout:
              - run:
                  name: Do this after checkout.
                  command: echo "Did this after checkout"
            before_build:
              - run:
                  name: Do this before the build.
                  command: echo "Did this before the build"
            after_build:
              - run:
                  name: Do this after the build.
                  command: echo "Did this after the build"
```

## Standard build and push
```yaml:examples/standard-build-and-push.yml
description: |
  A standard docker workflow, where you are building an image with a
  Dockerfile in the root of your repository, naming the image to be the
  same name as your repository, and then pushing to the default docker
  registry (at docker.io). Using the DOCKER_LOGIN set as default user

usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x

  workflows:
    build_and_publish_image:
      jobs:
        - kaniko-publish/publish
```

## With extra build args
```yaml:examples/with-extra-build-args.yml
description: >
  Build/publish an image with extra build arguments

usage:
  version: 2.1
  orbs:
    kaniko-publish: dre2004/kaniko-publish@x.x.x
  workflows:
    extra_build_args:
      jobs:
        - kaniko-publish/publish:
            extra_build_args: --build-arg FOO=bar --build-arg BAZ=qux
```
