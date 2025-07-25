[![VFX Platform](https://img.shields.io/badge/vfxplatform-2025%20%7C%202024%20%7C%202023%20%7C%202022-blue.svg)](http://www.vfxplatform.com/)
[![Python](https://img.shields.io/badge/python-3.11%20%7C%203.10%20%7C%203.9-blue.svg)](https://www.python.org/)
[![Build Status](https://dev.azure.com/shotgun-ecosystem/Toolkit/_apis/build/status/Apps/tk-multi-starterapp?branchName=master)](https://dev.azure.com/shotgun-ecosystem/Toolkit/_build/latest?definitionId=57&branchName=master)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Linting](https://img.shields.io/badge/PEP8%20by-Hound%20CI-a873d1.svg)](https://houndci.com)

# Welcome to the Flow Production Tracking Toolkit Starter App!
This app serves as a quick way to get started when doing Toolkit App development.
If you want to get up and running quickly, follow these simple steps:

## Step 1. Fork this Repository!
First of all, fork this repo. You can fork it to your own github accout or fork it to
an internal git server, that's totally up to you! At this time, make sure you also
rename it to something sensible. We recommend the naming convention `tk-ENGINE-APPNAME`,
where ENGINE is set to `multi` if the app can run in more than one engine. For example,
if you are working on a rigging tool in maya, you may want to name it `tk-maya-characterposer`.

## Step 2. Install your forked App in Toolkit

### Create a Dev Area
Now, first things first - before starting development, let's install the App. First, create a
development sandbox for your project by going to the pipeline configurations page in
Flow Production Tracking and click select "Clone" on the menu when right clicking on the primary
pipeline configuration. This will give you a private place to do development and you wont be
disturbing the production.

### Install the new repository
With your development sandbox there will be a specific tank command that you can use to address
this particular configuration.
1. Open a shell and navigate to your sandbox.
> cd /your/development/sandbox
2. Now run the install app command.
> ./tank install_app shot_step tk-maya user@remotehost:/path_to/tk-multi-mynewapp.git
3. When you install an app, you need to choose an environment and an engine.
- The engine is the application you will be running, so either `tk-maya`, `tk-nuke` etc.
- The environment is a collection of tools that you want to run against a specific work area.
In our default configuration, when working with **Shots**, the environment is called `shot_step` and when working with **Assets**, the environment is called `asset_step`.

```

```

This will find the latest git tag and install that into your setup. If you want more information
about how the install_app command works, just run it without any options.

Now, to test that the App was installed correctly, go to a Shot task in Flow Production Tracking
and launch maya from your development sandbox. Toolkit now tracks this repository and if you create
new tags, these will be detected by Toolkit's update system.

## Step 3. Set up your local environment

Now clone your forked repo locally, so that you have the code on disk somewhere. Next, we need
to switch toolkit so that it doesn't track the latest tag in the git repo, but instead looks
at your local code. For example, if you have your locally checked out code in `/Users/john.smith/dev/tk-multi-mynewapp`,
you would do the following:

```
> cd /your/development/sandbox
> ./tank switch_app shot_step tk-maya tk-multi-mynewapp /Users/john.smith/dev/tk-multi-mynewapp
```

## Step 4. Make changes!

Make changes to your code. Since you are now running tookit with a dev setup, there is a reload
option on the menu. Clicking this will reload all apps and configuration, making it easy and
quick to iterate.

## Step 5. Tag up a version and switch back to git mode

When you are ready to release, tag up a version in git. Name it for example `v1.0.0`.
Then, switch back to git mode. Toolkit will pick up the tag with the higest number
and use that - your dev area is no longer used by the system.

```
> cd /your/development/sandbox
> ./tank switch_app shot_step tk-maya tk-multi-mynewapp user@remotehost:/path_to/tk-multi-mynewapp.git
```

## Step 6. Push your config changes to the production config

Lastly, push your configuration changes to the Primary production config for the project.

```
> cd /your/development/sandbox
> tank push_configuration
```
