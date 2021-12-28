<div align="center">
  <h1>EAS in GitHub Actions</h1>
  <p>Build your apps with EAS, <i>without using EAS</i></p>
  <p>
    <a href="https://github.com/byCedric/gha/actions">
      <img src="https://img.shields.io/github/workflow/status/byCedric/eas-gha/Build%20App" alt="latest build" />
    </a>
    <a href="https://github.com/byCedric/eas-gha/blob/main/LICENSE.md">
      <img src="https://img.shields.io/github/license/byCedric/eas-gha" alt="license" />
    </a>
  </p>
  <p>
    <a href="https://github.com/byCedric/eas-gha#-structure"><b>Structure</b></a>
    &ensp;&mdash;&ensp;
    <a href="https://github.com/byCedric/eas-gha#-workflow"><b>Workflow</b></a>
    &ensp;&mdash;&ensp;
    <a href="https://github.com/byCedric/eas-gha#-how-to-use-it"><b>How to use it</b></a>
    &ensp;&mdash;&ensp;
    <a href="https://github.com/byCedric/eas-gha#%EF%B8%8F-caveats"><b>Caveats</b></a>
  </p>
</div>


## 📁 Structure

The app is based on the [tabs template](https://github.com/expo/expo/tree/master/templates/expo-template-tabs), just as example.

## 👷 Workflow

[The workflow](./.github/workflows/build.yml) is a simple GitHub Actions workflow using [expo-github-action](https://github.com/expo/expo-github-action), `eas build --local` command, and uploading artifacts to the workflow run.

## 🚀 How to use it

By default, the workflow is only running when you trigger it manually. But you can customize it however you like. Just make sure you are running the `eas build --local` command with the right `--platform` and `--profile` flags.

## ⚠️ Caveats

### Using macOS to support iOS builds

Ubuntu is the fastest environment of GitHub Actions, but to support iOS builds we need to use macOS. You can optimize this by changing the OS per platform.

### Colon in binary names

Right now, the local app binary has a name with a colon. `actions/upload-artifact` doesn't accept colon in files, so we need to rename it before uploading. ([more info here](https://github.com/expo/eas-build/issues/64))

### One platform per run

As of writing, the `eas build --local` command can only build a single platform per execution. You can run it multiple times in your workflow, but only for a single platform per run.

### Using local credentials in CI

If you want to fully disconnect from Expo services, you'll need to maintain the keystore or certificates yourself. You can do that by [configure EAS with local credentials](https://docs.expo.dev/app-signing/local-credentials/#credentialsjson). When your CI provider doesn't allow you to add "secret files", like GitHub Actions, you can [encode these files to base64 strings](https://docs.expo.dev/app-signing/local-credentials/#using-local-credentials-on-builds-triggered-from) and decode whenever you need it.

> It's highly recommended to keep keystores and certificates out of your repository to avoid security issues.


<div align="center">
  <br />
  with&nbsp;:heart:&nbsp;&nbsp;<strong>byCedric</strong>
  <br />
</div>
