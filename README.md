# `hashborg` -- Hook-driven Github automation for #!

This is (meant to be) a Github “integration” that provides various
organisations-wide services for #!, based on webhook notifications from
Github.


## Scope

All automation that consists in a short-lived process (not in the OS sense)
triggered by a Github event and is unprivileged.  This excludes CI/CD.


## Services

### On-commit notifications

Github's built-in IRC notifications must be set up on a per-repository
basis, and are fairly inflexible: this results in over-verbose
notifications in #!

This service notifies on each push to `master` on any repository,
distinguishing 3 cases:

1. The push merges one or more pull requests.
   In this case, only the pull requests are mentioned in the notification,
   not each individual commit.

2. The push is not fast-forward (i.e. someone “force pushed”)

3. The push is fast-forward and does not merge pull-requests.


Moreover, notifications are sent whenever a new issue or pull request
is opened or closed (in the later case, without duplication with
commit notifications).


### Issues/PR assignment

Having issues and pull requests lying around without any acknowledgement
is fairly disheartening for the user who submitted it.  To prevent that,
this service automatically assigns someone to each new review and PR,
and notifies the assignee by email.

The notification email contains a reminder of what assignees should do:
- leave a message to the original poster;
- triage the bug/PR and set appropriate labels;
- mention contributors who might be interested or able to help.

Moreover, it contains a summary of some [helpful advice] on how to
treat new issues and pull requests, namely:
- respond quickly;
- thank the original poster;
- start by describing the positive aspects of the contribution;
- try to find a path to accepting the contribution rather than rejecting it;
- provide clear, actionable feedback;
- be effusive.

[helpful advice]: https://brson.github.io/2017/04/05/minimally-nice-maintainer
