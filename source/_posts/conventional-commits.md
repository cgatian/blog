---
title: Conventional Commits
date: 2017-03-28 20:07:57
tags: Git, Dev Tools
---

If you've been following the recent Angular release canidates you can't help but admire the changelog they are able to produce. Each version published has a nicely formated list of bugs, features, and breaking changes. How they were able to generate this type of changelog really interested me into digging deeper into their process and conventions. It turns out, implementing something like this into your workflow is actually quite simple.

### Standarizing Commit Messages
The first step is to start utilizing a convention when commiting changes to your codebase. The easiest way is to use the [conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/preview) created by the AngularJS team.

A more readable form of this can be found from Angular Material team's [Code Convention Guidelines](https://github.com/angular/material2/blob/master/CONTRIBUTING.md#-commit-message-guidelines). At a minimum, each commit message contains a *type*, *scope* and *subject*.  In the following format:

```
<type>(<scope>): <subject>
```

### Add Tooling
Making sure we commit changes using this format can be teadius at first. To make life easier add [Commitizen](http://Commitizen.github.io/cz-cli/) as a development dependency.  This provides a command line utlity that will walk you through each portion of the commit message.

Install commitizen
```
yarn add commitizen -D
```
Add [conventional-cz](https://github.com/commitizen/cz-conventional-changelog)
```
yarn add cz-conventional-changelog -D
```

Update `package.json`
First add a new script named commit which executes `git-cz` (Commitizen)
```
scripts : {
    "commit": "git-cz"
    ...
}
```
Then add an additional block called config
```
"config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
}
```
Stage your changes by running `git add .` followed by `npm run commit`.
{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1490656960/conventional-commits1_fc70yy.gif %}

Success!

### Preventing Poor Commit Messages
Having this tooling is great, but what about that one developer that just doesn't seem to get it and is stuck in their ways? Thankfully, preventing commits that do not meet the convention is simple to do by installing a [git hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks). But to be honest, I've never configured a Git hook. Thankfully, [Husky](https://github.com/typicode/husky) makes configuration painless.

First install Husky:
```
yarn add husky -D
```

Next install [validate-commit-msg](https://github.com/kentcdodds/validate-commit-msg)
```
yarn add validate-commit-msg -D
```

Update your `package.json` scripts:
```
scripts: {
    "commitmsg": "validate-commit-msg"
}
```
Now any commit messages that do not follow the convention will error to the developer.

{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1490660503/conventional-commits2_vgu3nh.gif %}


### Generating a Changlog and Versioning
Now that our project is setup lets see the added benefits this provides. To kick off the next step we are going to install `standard-version`. This plugin not only will generate the proper version for our project, but it will also create a change log with proper commit hashes, and issue numbers. 

Install standard-version
```
yarn add standard-version -D
```
Update your `package.json` scripts:
```
scripts: {
    "release": "standard-version"
}
```
Run `npm run release`. This will examine your Git history and based off your commits generate the proper version and a CHANGELOG.md.
***
### Demoing This Process to Your Team
To help demo how this would work in the real world, I've setup a repository with everything configured. First [fork this repository](https://github.com/devboosts/conventional-commits).

With the newly forked project lets enable Issue tracking. This will give us a feel for how this would work when we collaborate on a real project.

* Open the project's settings in GitHub and enable **Features > Issues**
* Create a new issue called **feat: Implement Footer**
* Clone your forked repository
* Verify you're in the newly created directory and run `npm install` (or `yarn`)
* Create a new branch by running `git branch feat/footer`
* Open `./src/index.html` and add a `footer` element
* Save your changes
* From the CLI run `git add .` followed by `npm run commit`

Follow the prompts adding, using the following information:
```
type:feature
scope: index
short description: added a footer
long description: <empty>
breaking changes: <empty>
issues closed: <enter your issue number ie. #1>
```
* Push your changes to GitHub with `git push`
* Next open a pull request and merge your changes in

Notice the `CHANGELOG.md` and `package.json` version are unchanged.  The reason they haven't been updated is because we need to first cut a release. Let's do that now.

* From your command line switch back to master by running `git branch master`
* Pull in your latest changes by running `git pull`
* Run `npm run release`

This runs [standard-version](https://github.com/conventional-changelog/standard-version) which examines your commit history to properly update the `CHANGELOG.md`, version in `package.json`, and tags a branch in your repository.
Finally, run `git push --follow-tags origin master` to push your version changes and tag your repository with this version.

### Beyond...
Checkout this great [plugin](https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-commitizen) for VSCode. It integrates with commitizen and provides a wizard like experience.

I haven't actually tried this out yet, but to take things to the next level you could look into [semantic-release](https://github.com/semantic-release/semantic-release). It promises fully automated packaging and releasing.  Basically, what standard-version does, with the added benefit of integrations with GitHub and Travis CI.