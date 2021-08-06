---
title: "Introducing: Armv8 Equinix-Metal, super fast builds for OSS"
created_at: Fri Aug 06 2021 15:00:00 EDT
author: Montana Mendy
layout: post
permalink: 2021-08-07-oss-equinix
category: news
excerpt_separator: <!-- more --> 
tags:
  - news
  - feature
  - infrastructure
  - community
---

![Opt  1](https://user-images.githubusercontent.com/20936398/128098661-1f3ef330-55d0-4de8-b91a-d40e1ff912bd.png)

In October 2019, Travis CI, ARM and Equinix Metal (previously called Packet) partnered to enable cloud CI/CD builds on previously unavailable CPU architecture targets, starting with Armv8. Infrastructure sponsored by ARM and set up thanks to the effort of Canonical LXD, Equinix and Travis CI teams was employed to run fast-starting, LXD container based build jobs over arm64. In the meantime a lot happened and it became apparent that faster Armv8 CPUs are needed.

<!-- more --> 

Well to answer your question, here they are. Just add this in your `.travis.yml` file:

```yaml
os: linux
arch: arm64
```

That will now tell Travis to use the super fast new generation of `arm64` CPU based servers, deployed by Equinix for Travis CI. This is is free to use for OSS (build minute costs zero credits if you run a build over your open source repository) as a part of our [Partner Queue Solution](https://docs.travis-ci.com/user/billing-overview/#partner-queue-solution). This infrastructure is not available for builds over private/proprietary source code.

## What is it and the benefit

The infrastructure upgrade allows Armv8 builds in LXD containers to spin up much faster. The performance improvement proved impressive, as Montana Mendy found out after taking the new environment for a test drive.

## Build study conducted by Montana Mendy

Below is a graph of a study conducted by Montana Mendy, where he took the same exact repository which is [here](https://github.com/Montana/travis-staging-arm64). It's a breadth-first search application Montana wrote in Python who has made it open source solely for this post, and in this repository you can see the `.travis.yml`, the `.travis.yml` did not differ for builds, in other words - nothing was changed when running the builds with Equinix-Metal and when the builds were ran on the previous architecture. 

<img width="1048" alt="buildtimes" src="https://user-images.githubusercontent.com/20936398/128437785-02d77fb5-835d-408d-937e-4873bddcce25.png">

As you can see with Equinix-Metal it's twice as fast, now remember this is building a small grade project. Imagine the time you'll save when the proejct is a tad bigger. I've attached more references as it relates to build times:

**Build times when using Equinix-Metal:**

<img width="1458" alt="equinix" src="https://user-images.githubusercontent.com/20936398/128438474-a41b0498-c90e-4828-a712-e3bd27ca6b06.png">

**Build times when the end user is not using Equinix-Metal:**

<img width="1431" alt="without" src="https://user-images.githubusercontent.com/20936398/128438586-11b04bd5-dbf1-41a6-8323-a2be628412c5.png">

To state once more, I've left [repository](https://github.com/Montana/travis-staging-arm64) link on GitHub that I used to measure these times, so you can see exactly my `.travis.yml` configuration and other things that make sense to you. 

## Conclusion

Right now it actually doesn’t matter which one of [Arm infrastructures available at Travis CI](https://docs.travis-ci.com/user/multi-cpu-architectures/#multi-cpu-availaibility) you use: all are powered by modern, performant CPUs. Enjoy faster build times over Armv8 as well, we are sorry to make your coffee and tea breaks shorter!

## Where to find out more

You can find out more about the new Arm on AWS Graviton2 integration by reading about the [Travis CI build environment](https://docs.travis-ci.com/user/reference/overview/) and building on [multi-CPU architectures](https://docs.travis-ci.com/user/multi-cpu-architectures). Be sure to leave your feedback and join the discussion over at the [community forum](https://travis-ci.community/c/integrations/aws-graviton2/102). If you have any questions do not hesitate to post on the forums or contact [montana@travis-ci.org](mailto:montana@travis-ci.org).

Not a Travis CI user yet? [Sign up for a free trial](https://travis-ci.com/signup?utm_source=tciblog&utm_medium=blogpost&utm_campaign=blog_cta)!

Looking for something more _bespoke for your builds?_ Try out [Travis CI Enterprise](https://travis-ci.com/plans?anchor=enterprise-section&utm_source=tciblog&utm_medium=blogpost&utm_campaign=blog_cta).

## Ref blog posts:

[Multi-CPU architecture support for your builds - Oct 2019](https://blog.travis-ci.com/2019-10-07-multi-cpu-architecture-support).

[Build your open source projects on IBM Power and IBM Z CPU architecture - Nov 2019](https://blog.travis-ci.com/2019-11-12-multi-cpu-architecture-ibm-power-ibm-z).

[Announcing General Availability of Graviton2 CPU Support! - Nov 2020](https://blog.travis-ci.com/2020-09-11-arm-on-aws).
