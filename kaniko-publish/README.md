# Kaniko Publish Orb

This is a fork of the Kaniko Publish Orb originally created by [Glenjamin](https://github.com/glenjamin/). 

| Component | Version |
|:---------:|--------:|
| kaniko    | v1.7.0  |
| debian    | 11-slim (bullsye) |


Build and publish container images to container registries *without* docker

Under the hood this uses Google's [Kaniko](https://github.com/GoogleContainerTools/kaniko) project, but aims to provide a very similar interface to the [circleci/docker-publish](https://circleci.com/orbs/registry/orb/circleci/docker-publish) orb.

## Usage

See https://github.com/dre2004/orbs/tree/master/kaniko-publish for the full details.

```
orbs:
  kaniko-publish: dre2004/orbs/kaniko-publish@x.x.x

workflows:
  flow:
    jobs:
      - kaniko-publish/publish
```

## Credits

- [Glenjamin](https://github.com/glenjamin/) the original creator of this Orb [Kaniko Publish Orb](https://github.com/glenjamin/kaniko-publish-orb/)
- [freeletics](https://github.com/freeletics/) created an updated version of the Orb