<!--
{% comment %}
Copyright 2018-2020 Elyra Authors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->

# Project Contribution Guidelines

This guide documents the best way to make various types of contribution to the Elyra projects,
including what is required before submitting a documentation or code change and how to properly merge them.

Contributing to the Elyra project doesn't just mean writing code. Helping testing and reviewing pull requests
and improving documentation are also welcome. In fact, proposing significant code changes usually requires first
gaining experience and credibility within the community by helping in other ways. This is also a guide to 
becoming an effective contributor.

The following items will be discussed in this document :

* [Contributing Documentation Changes](#Contributing+Documentation+Changes)
* [Contributing code changes](#Contributing+code+changes)
  * [Before creating a Pull Request](#Before+creating+a+Pull+Request)
  * [Creating a Pull Request](#Creating+a+Pull+Request)
  * [The Review Process](#The+Review+Process)
  * [Merging Pull Requests](#Merging+Pull+Requests)


# Contributing Documentation Changes

To create or modify the project documentation, edit the Markdown source files which is usually located at
$project/docs directory, whose README file shows how to build the documentation locally to test your changes.

The process to propose a doc change is otherwise the same as the process for proposing code changes below.

# Contributing code changes

Please review the following section before proposing a code change. This section documents how to do so.

***
**When you contribute code, you affirm that the contribution is your original work and that you license the
work to the project under the project's open source license.**

**Whether or not you state this explicitly, by submitting any copyrighted material via pull request, email,
or other means you agree to license the material under the project's open source license and warrant that you
have the legal authority to do so.**
***


## Before creating a Pull Request

1. Make sure you have the most up to date code

If you haven't done so, please set upstream as described in [GitHub Documentation](https://help.github.com/articles/configuring-a-remote-for-a-fork/)

Make sure you do not have any uncommitted changes and rebase main with latest changes from upstream:

```
git fetch upstream
git checkout main
git rebase upstream/main
```

Now you should rebase your branch with main, to receive the upstream changes:

```
git checkout branch
git rebase main
```

In both cases, you can have conflicts:

```
error: could not apply fa39187... something to add to patch A

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
Could not apply fa39187f3c3dfd2ab5faa38ac01cf3de7ce2e841... Change fake file
```

Here, Git is telling you which commit is causing the conflict (fa39187). You're given three choices:

* You can run `git rebase --abort` to completely undo the rebase. Git will return you to your branch's
state as it was before git rebase was called.
* You can run `git rebase --skip` to completely skip the commit. That means that none of the changes
introduced by the problematic commit will be included. It is very rare that you would choose this option.
* You can fix the conflict.

To fix the conflict, you can follow [the standard procedures for resolving merge conflicts from the command line](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line). 
When you're finished, you'll need to call `git rebase --continue` in order for Git to continue processing
the rest of the rebase.

> **Note:** If there are any merge conflicts with the `yarn.lock` file, there is 
> no need to manually resolve them. Simply run `yarn install` and yarn will do its
> best to automatically resolve any conflicts.

## Creating a Pull Request

1. Set up SSH if you haven't already, or generate a new SSH key if necessary as described in the [Github Documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
1. Fork the Github repository at https://github.com/elyra-ai/xxx if you haven't already.
1. Clone your fork, create a new branch, push commits to the branch.
     * Below is a vague outline of the commands to be followed when doing these steps:
          * Cloning your fork:
               * git clone https://github.com/<your-github-id>/<desired-elyra-repository>.git
               * Set `upstream` as described in the [GitHub documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-for-a-fork)
          * Creating a new branch:
               * git checkout -b <branch-name>
          * Committing and pushing a file:
               * git add <file-name>
               * git commit
                    * Opens a text file that is a summary of the current commit operation
                    * Add a commit message that describes the changes you made
                    * Ctrl + X and enter to save
               * git push
                    * Pushes the commit from your local repo to the remote repo
1. Consider whether documentation or tests need to be added or updated as part of the change, and add them as needed.
1. Open a pull request against the main branch of elyra-ai/elyra. (Only in special cases would the PR be opened 
   against other branches.)
  1. The PR title should describe the proposed change in the PR itself.
  1. If the pull request is still a work in progress, and so is not ready to be merged, but needs to be pushed 
     to Github to facilitate review, then prefix the PR title with `[WIP]`.
  1. Follow [The 7 rules for a great commit message](http://chris.beams.io/posts/git-commit/)
     * Separate subject from body with a blank line
     * Limit the subject line to 50 characters
     * Capitalize the subject line
     * Do not end the subject line with a period
     * Use the imperative mood in the subject line
     * Wrap the body at 72 characters
     * Use the body to explain what and why vs. how

## The Review Process


The review process can help the project achieve a high-quality code base. When performing code reviews,
various aspects should be considered, and this
[code review checklist](https://www.michaelagreiler.com/wp-content/uploads/2019/08/Code_Review_Checklist_Greiler.pdf)
gives some examples of such items.

What to expect from the review process?

* Other reviewers, including committers, may comment on the changes and suggest modifications. Changes can be added
  by simply pushing more commits to the same branch.
* Lively, polite, rapid technical debate is encouraged from everyone in the community. The outcome may be a
  rejection of the entire change.
* Reviewers can indicate that a change looks suitable for merging with a comment such as: 
  "I think this patch looks good". Elyra uses the LGTM convention for indicating the strongest level of 
  technical sign-off on a patch: simply comment with the word "LGTM". It specifically means: 
  "I've looked at this thoroughly and take as much ownership as if I wrote the patch myself". If you comment LGTM 
  you will be expected to help with bugs or follow-up issues on the patch. Consistent, judicious use of LGTMs
  is a great way to gain credibility as a reviewer with the broader community.
* Sometimes, other changes will be merged which conflict with your pull request's changes. The PR can't be merged
  until the conflict is resolved. This can be resolved with "git fetch origin" followed by "git merge origin/main" 
  and resolving the conflicts by hand, then pushing the result to your branch.
* Try to be responsive to the discussion rather than let days pass between replies.

## Merging Pull Requests

To avoid a convoluted main branch history, with lots of "merge xxx" on the commit history, we are not using the
GitHub `merge pull request` UI option and recommending either `squash and merge` or `rebase and merge` options. 
