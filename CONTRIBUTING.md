*(This document uses [RFC 2119][rfc2119] keywords.)*

Pull Requests
-------------

1.  Commit messages **MUST** use [this format][commit-format] and [this
    style][commit-style].

1.  Pull requests **MUST** be about only one topic.

    This way, changes can be seen and discussed individually.

1.  Pull requests **MUST** be **rebased** on the latest **master** from the
    **upstream** repository:

    ```bash
    # add the upstream repository as remote
    git remote add upstream \
      https://github.com/idiv-biodiversity/ansible-role-systemd-timesyncd.git

    # fetch latest upstream commits
    git fetch upstream

    # rebase your branch on master
    git rebase upstream/master topic/name

    # force push the changed history
    # this will automatically update the pull request
    git push --force origin topic/name
    ```

1.  Pull requests **SHOULD NOT** be done in **master**:

    ```bash
    git switch -c topic/name
    ```

    This is not strictly necessary for small changes, e.g. fixing typos in
    `README.md`.


[commit-format]: https://idiv-biodiversity.github.io/git-knowledge-base/commit-message-conventions.html#structural-style
[commit-style]: https://idiv-biodiversity.github.io/git-knowledge-base/commit-message-conventions.html#wookietreiber
[rfc2119]: https://tools.ietf.org/html/rfc2119
