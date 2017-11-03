# References

## Table of Contents
1. [Artifactory](#artifactory)
    * [Setup with NPM](#setup-with-npm)
    * [Creating a new package](#creating-a-new-package)
2. [Concourse](#concourse)
    * [Setting up Concourse](#setting-up-concourse)
    * [Using Concourse](#using-concourse)

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
