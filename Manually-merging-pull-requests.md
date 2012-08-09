_This page serves as a simple "how to" for Spring committers when manually merging pull requests from contributors._

# Placeholders

Many of the `git` commands listed below contain placeholders as defined below.

- `<ACCOUNT>`: GitHub account for the author of the pull request
- `<BRANCH>`: branch in pull request author's account (e.g., SPR-####)
- `<PULL_REQUEST_NUMBER>`: spring-framework pull request number

### Example

To determine the values for these placeholders, let's take a look at [pull request #111](https://github.com/SpringSource/spring-framework/pull/111) as an example. From the pull request page you should be able to find an example `git` command for pulling the request into your local working directory. For example, if you click on the _info_ icon in the "This pull request can be automatically merged" bar, you should see something like `git pull git://github.com/sbrannen/spring-framework.git SPR-9492`. From this information we determine the placeholder values to be the following.

- `<ACCOUNT>`: sbrannen
- `<BRANCH>`: SPR-9492
- `<PULL_REQUEST_NUMBER>`: 111

# Performing the Merge

## Set up remote, fetch branch, and rebase

```shell
git co master
git remote add <ACCOUNT> https://github.com/<ACCOUNT>/spring-framework.git
git fetch <ACCOUNT>
git co --track <ACCOUNT>/<BRANCH> -b <BRANCH>
git rebase master
```

## Modify working directory

- polish, format, refactor, document, update changelog, etc.
  - see the [[Contributor guidelines]] for details
- once changes are finalized and committed to the branch, squash commits
  into a single commit. For example: `git rebase --interactive --autosquash`

## Merge into master and push

```shell
git co master
git merge --no-ff --log -m "Merge pull request #<PULL_REQUEST_NUMBER> from <ACCOUNT>/<BRANCH>" <BRANCH>
git push springsource master:master
```

# Cleaning Up

## Update remote pull request branch to rebased/modified version (optional)

_This is only possible if you have write permissions for the remote repository -- for example, if you are merging your own pull request._

```shell
git push --force <ACCOUNT> <BRANCH>
```

## Delete remote pull request branch (optional)

_This is only possible if you have write permissions for the remote repository -- for example, if you are merging your own pull request._

```shell
git push <ACCOUNT> :<BRANCH>
```

## Delete local branch (optional)

```shell
git branch -D <BRANCH>
```

## Delete local remote entry (optional)

```shell
git remote rm <ACCOUNT>
```