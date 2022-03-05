---
published: true
date: 2022-03-05 00:23:00 +0100
last_modified_at: 2022-03-05 00:23:00 +0100
title: Automate Test-Coverage Badge status on Github
description: >-
  A quick tutorial showing how to commit and push files to a remote git repository from a Github actions / workflows. Ex: Automation of publishing the ReportGenerator test coverage badge after a successful test.
comments: true
categories:
  - How To
tags:
  - github
  - tutorial
  - automation
  - cliargs
image:
  src: /Content/Images/auto-push-reportgenerator-badge.png
  width: 800
  height: 500
fullview: true
toc: true
---
![Cliargs.NET Coverage](https://raw.githubusercontent.com/wiki/YounesCheikh/Cliargs.NET/combined.svg){: .right }
When I decided to share the source code of [`Cliargs.NET`][1] library on Github, I wanted to show some statistics badges on the README file, such as the count of downloads, the build status... and finally the test coverage.

# Background
I am using [ReportGenerator][2] from [Daniel Palme][3] which is really a great tool to have a full report about the test coverage for lines / branches. So I set up the [Github Action][4] to get the test coverage report generated after each commit. This action uploads the artifacts to the build results (which is good actually), however these artifacts are uploaded in a zip file (Limitation from Github 😏).

The limitation I faced here, is there is no way to get a direct link to the generated badge svg file to get it displayed on the readme file. So I had to find a way to upload the badge file automatically after the report is generated, to another remote Git repository in order to ensure having a direct link to the badge from the readme file.

# Step by step

> If you are familiar with Git, Github workflows, you may jump to the [last section](#implement-all-in-your-workflow) and copy the code without reading the detailed step by step explanation.
{: .prompt-info}

## Choice of remote git repository

![Clone Github Wiki]({{ site.ImagesFolder }}/Github-wiki-clone.png){: .shadow }
_Github Wiki Git Url_

In my case I have created a [Wiki][5] to add a documentation of Cliargs.NET. A Wiki of Github reposiotry is another Git repository with a different address, usually `https://github.com/[Username]/[Repository Name].wiki.git`.

Nevertheless, there are tons of other ways to get a public Git repository, for me the easiest way is [Gist][6]!

![Clone Github Wiki]({{ site.ImagesFolder }}/Gist-clone.png){: .shadow }
_Gist repository url_

> Each Gist is a Git repository, with an address `https://gist.github.com/[Unique Id].git`, so you just clone the repository and start commiting changes.


## Create a Personal Access Token
Of course it is not a good idea to write your password in a Workflow file, so you need to generate a new personal access token from [`Github Settings > Developer settings > Personal access tokens`][7] then click generate new token.
> Each token has a defined scopes, chose the ones you prefer. For this example, we need a commit / push permissions. Once the token is generated, make sure to copy it and save it somewhere immediately as it will not be visible again!
{: .prompt-tip }

## Create an encrypted secret
At this step we need to create a Github secret to be able to call the generated personal access token from the Workflow using the secret name instead of pasting the token into the Workflow file for security reasons.

Navigate to your repository settings (The repository from where the action will be executed), `https://github.com/[Username]/[Repository name]/settings` then navigate on the left sidebar to `Secrets > Actions`.

![Clone Github Wiki]({{ site.ImagesFolder }}/github-new-secret.png){: .shadow }
_Github Repository new secret_

Choose a good name and save it somewhere because you'll need it later.

## Add file to a repository

In my case, I had to run first the [job of ReportGenerator][4], then recover the generated badge before pushing.
But in the following example, to make it easier, I choose to download the Cliargs.NET icon using `curl` then push it back to a remote repository.

### Checkout a remote repository

Here we need to checkout the remote repository and change the working directory to the repository local folder.
```shell
git clone https://github.com/[Github Username]/[Repository Name].git
cd [Repository Name]
```

### Add file to local repository directory
As explained above, I download the file from web named `Cliargs.png`, but in your case you may need to move the file from another location to the local repo directory.

```shell
curl https://raw.githubusercontent.com/YounesCheikh/Cliargs.NET/main/Cliargs.png --output Cliargs.png
```

### Configure git credentials
Here is very important to don't set the password, only set the username and email to identify the author to git server when pushing changes.

> If your repository is public, better don't set the email, otherwise, you will get spammed, In my case i just keep it empty. 😉
{: .prompt-warning }

```shell
git config credential.helper store
git config user.name "Your name"
git config user.email "<>"
```

### Set the git url
The tricky here is to use the git set-url in order to use your personal access token instead of your password!
At this step you're supposed to get the [personal access token generated](#create-a-personal-access-token) and the [repository secret saved](#create-an-encrypted-secret).
{% raw %}
The call to your saved secret is called in format `${{ secrets.[Github Secret] }}`

```shell
git remote set-url origin https://${{ secrets.[Github Secret] }}@github.com/[Github Username]/[Remote  name].git
```
{% endraw %}

### Commit the changes and push

```shell
git add `Cliargs.png`
git commit -m "updated file"
git push
```

## Implement all in your Workflow

Now you followed the step by step above, it is time to append the global code in your Workflow yml file.

{% raw %}
```yaml
    - name: Upload file to remote git repo
      run: |
        git clone https://github.com/[Github username]/[Respository name].git
        cd [Respository name]
        git config credential.helper store
        git config user.name "[Your name]"
        git config user.email "<>"
        git remote set-url origin https://${{ secrets.[Secret name] }}@github.com/[Github username]/[Respository name].git
        curl https://raw.githubusercontent.com/YounesCheikh/Cliargs.NET/main/Cliargs.png --output Cliargs.png
        git add Cliargs.png
        git commit -m "updated file"
        git push
```
{% endraw %}

# Conclusion
For me, I have reached the target with the several lines above, and the test coverage badge is well shown on the repository home page (readme file). May be in the future, I will try to share something more advanced, such as create a Github Action that automate all the steps above.

[1]: https://github.com/YounesCheikh/Cliargs.NET "Cliargs.NET on Github"
[2]: https://github.com/danielpalme/ReportGenerator "Report Generator Github Repository"
[3]: https://www.palmmedia.de "Daniel Palme"
[4]: https://github.com/marketplace/actions/reportgenerator "ReportGenerator Github Action"
[5]: https://github.com/YounesCheikh/Cliargs.NET/wiki "Cliargs.NET wiki"
[6]: https://gist.github.com "Gist"
[7]: https://github.com/settings/tokens "Github Personal Access Tokens"
