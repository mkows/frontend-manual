# References

## Table of Contents
1. [Artifactory](#artifactory)
    * [Setup with NPM](#setup-with-npm)
    * [Creating a new package](#creating-a-new-package)
2. [Concourse](#concourse)
    * [Setting up Concourse](#setting-up-concourse)
    * [Using Concourse](#using-concourse)
3. [Automation](#automation)
4. [Terraform](#terraform)
    * [Quick Reference](#tf-quick-reference)

## Artifactory

> We use [Artifactory](https://www.jfrog.com/artifactory/) to store all our internal NodeJS packages. This is equivalent to using [npm Enterprise](https://www.npmjs.com/enterprise).

### Setup with NPM

To access the [Artifactory web interface](https://hbc.jfrog.io/hbc/webapp/), you will need to authenticate through [Okta](https://hbctech.okta.com/).

1. Once authenticated to Artifactory, click on your username in the top right where it says, "Welcome, _username_".
2. From the User Profile page, click Generate (gear icon) to generate your API key.
3. Click the green `Save` button in the bottom right.
4. Click the Artifactory logo on the top left to go back to the homepage.
5. In the middle the Artifactory homepage in the `Set Me Up` widget, filter by `hbc-virt-npm`. Then click `hbc-virt-npm`.
6. Copy the code in the `Using basic authentication` section. (It includes `auth`, `email`, and `always-auth` keys)
7. Open `~/.npmrc` in your text editor of choice and replace the contents of the file with your copied code.
8. Update the `email` key to match your HBC email.
9. Append `registry=https://hbc.jfrog.io/hbc/api/npm/hbc-virt-npm/` to your npmrc file.
10. Save your changes; you're all set up!

### Creating a new package

When creating a new npm package that will be shared internally (published to Artifactory), you should always define a `publishConfig` in your package.json file. This ensures your package is always and only published to Artifactory.

Simply add the following to your _package.json_ file:

```
"publishConfig": {
  "registry":"https://hbc.jfrog.io/hbc/api/npm/hbc-virt-npm"
}
```

## Concourse

> Concourse is the continuous integration / continuous deployment (CI/CD) we use at HBC Tech. [Learn more...](http://concourse.ci)

### Setting up Concourse

[Fly](https://github.com/concourse/fly) is the command line interface for Concourse. You will need to use _fly_ if you want to create/update/delete pipelines/jobs/tasks.

1. Navigate to your Concourse instance in a browser, and click the Apple icon.
2. Move the downloaded file to your`/Applications` folder.
3. Add it to your PATH by executing the command in your terminal:
```sh
install ~/Downloads/fly /usr/local/bin
```
4. Confirm _fly_ is working with `fly --version`.

### Using Concourse

Have a question about using Concourse? Add your question and the answer you find here!

## Automation

Anything you find yourself repeating over and over again is a great candidate for automation. We rely on [Concourse](#concourse) to automate most things, and so we've created several pipelines to handle common tasks.

Learn more about our shared [frontend pipelines](https://github.com/saksdirect/frontend-pipelines).

You may have seen some or all of these badges in our repos. So, here's what they each mean:

<!--* [![hbc undefined](https://img.shields.io/badge/hbc-undefined-00704A.svg)]()

  We don't have a use for this beautiful tag yet.

  Embed code:
  ```md
  [![hbc undefined](https://img.shields.io/badge/hbc-undefined-00704A.svg)]()
  ```

* [![hbc undefined](https://img.shields.io/badge/hbc-undefined-9C1B09.svg)]()

  We don't have a use for this beautiful tag yet.

  Embed code:
  ```md
  [![hbc undefined](https://img.shields.io/badge/hbc-undefined-9C1B09.svg)]()
  ```
-->

* [![hbc autoversion](https://img.shields.io/badge/hbc-auto--version-EFB412.svg?colorA=AAAAAA)]()

  The _auto-version_ badge indicates that a repo automatically increments its version on each new commit / merge to master.

  _How it works:_

  On each new commit / merge to master, our bot looks at the most recent commit's message (or pull-request title). Let's call this `message`.
    + If `message` contains `[breaking]`, implying that there is a breaking change in the code, our bot will increment the major version.
    + If `message` contains `[feature]`, implying that a feature was added in the code, our bot will increment the minor version.
    + Otherwise, our bot will increment the patch version.

  For more information on versioning, see [SemVer](http://semver.org/).

  _Note: You can also choose to skip auto-version if `message` contains `[ci skip]`._

  Embed code:
  + markdown:
  ```md
  [![hbc autoversion](https://img.shields.io/badge/hbc-auto--version-EFB412.svg?colorA=AAAAAA)](https://github.com/saksdirect/frontend-manual/tree/master/references#automation)
  ```
  + html:
  ```html
  <a href="https://github.com/saksdirect/frontend-manual/tree/master/references#automation">
      <img src="https://img.shields.io/badge/hbc-auto--version-EFB412.svg?colorA=AAAAAA" alt="hbc auto-version (learn more)">
  </a>
  ```

* [![hbc autopublish](https://img.shields.io/badge/hbc-auto--publish-0B4580.svg?colorA=AAAAAA)]()

  The _auto-publish_ badge indicates that a repo automatically publishes to [Artifactory](#artifactory) on each new commit / merge to master.

  _Note: You can also choose to skip auto-publish if the commit / pull-request title contains `[ci skip]`._

  Embed code:
  + markdown:
  ```md
  [![hbc autopublish](https://img.shields.io/badge/hbc-auto--publish-0B4580.svg?colorA=AAAAAA)](https://github.com/saksdirect/frontend-manual/tree/master/references#automation)
  ```
  + html:
  ```html
  <a href="https://github.com/saksdirect/frontend-manual/tree/master/references#automation">
      <img src="https://img.shields.io/badge/hbc-auto--publish-0B4580.svg?colorA=AAAAAA" alt="hbc auto-publish (learn more)">
  </a>
  ```

We should strive to use these features when applicable and display these badges so engineers can immediately know which features are being used.

## Terraform

> Terraform allows us to create infrastructure as code. [Learn more...](https://www.terraform.io/)

### <a name="tf-quick-reference"></a>Quick Reference

* _Are there any existing templates that I can use for my frontend application?_

    **Yes! Our shared terraform modules are in the [frontend-terraform](https://github.com/saksdirect/frontend-terraform) repo.**
