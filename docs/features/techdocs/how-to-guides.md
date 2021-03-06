---
id: how-to-guides
title: TechDocs "HOW TO" guides
sidebar_label: "HOW TO" guides
description: TechDocs "HOW TO" guides related to TechDocs
---

## How to use URL Reader in TechDocs Prepare step?

If TechDocs is configured to generate docs, it will first download the
repository associated with the `backstage.io/techdocs-ref` annotation defined in
the Entity's `catalog-info.yaml` file. This is also called the
[Prepare](./concepts.md#techdocs-preparer) step.

There are two kinds of preparers or two ways of downloading these source files

- Preparer 1: Doing a `git clone` of the repository (also known as Common Git
  Preparer)
- Preparer 2: Downloading an archive.zip or equivalent of the repository (also
  known as URL Reader)

If `backstage.io/techdocs-ref` is equal to any of these -

1. `github:https://githubhost.com/org/repo`
2. `gitlab:https://gitlabhost.com/org/repo`
3. `bitbucket:https://bitbuckethost.com/project/repo`
4. `azure/api:https://azurehost.com/org/project`

Then Common Git Preparer will be used i.e. a `git clone`. But the URL Reader is
a much faster way to do this step. Convert the `backstage.io/techdocs-ref`
values to the following -

1. `url:https://githubhost.com/org/repo/tree/<branch_name>`
2. `url:https://gitlabhost.com/org/repo/tree/<branch_name>`
3. `url:https://bitbuckethost.com/project/repo/src/<branch_name>`
4. `url:https://azurehost.com/organization/project/_git/repository`

Note that you can also provide a path to a non-root directory inside the
repository which contains the `docs/` directory.

e.g.
`url:https://github.com/backstage/backstage/tree/master/plugins/techdocs-backend/examples/documented-component`

### Why is URL Reader faster than a git clone?

URL Reader uses the source code hosting provider to download a zip or tarball of
the repository. The archive does not have any git history attached to it. Also
it is a compressed file. Hence the file size is significantly smaller than how
much data git clone has to transfer.

Caveat: Currently TechDocs sites built using URL Reader will be cached for 30
minutes which means they will not be re-built if new changes are made within 30
minutes. This cache invalidation will be replaced by commit timestamp based
implementation very soon.
