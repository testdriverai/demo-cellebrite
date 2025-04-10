# TestDriver - Web Quickstart

TestDriver is an AI QA Agent for GitHub. TestDriver allows you to run UI tests on your software using plaintext prompts. Every TestDriver test spawns an ephemeral VM and uploads the results to [Dashcam](https://dashcam.io) for easy debugging.

# Getting Help

TestDriver is made by [Dashcam](https://dashcam.io). Please [join the Dashcam discord for support and questions](https://discord.gg/6TUKZdfCze).

# Getting Started

## Fork This Template Repository

This template repository has the recommended settings for testing websites in Google Chrome with TestDriver. Begin by forking this template repository. Make the repository public or invite the Dashcam staff into your private repository so we can better support you.

<img width="208" alt="CleanShot 2024-03-08 at 16 59 12@2x" src="https://github.com/dashcamio/testdriver-web/assets/318295/b3d6970b-38ba-4a59-9f4c-c9a90a4047e5">

## Add your prompt to the GitHub Action

Dashcam is powered by [our TestDriver GitHub Action](https://github.com/dashcamio/testdriver), there are more details there outlining how TestDriver works. Add your test steps to the `.github/workflows/pr.yml` file under `prompt`.

```yml
name: TestDriver.ai

jobs:
  test:
    name: "TestDriver"
    runs-on: ubuntu-latest
    steps:
      - uses: dashcamio/testdriver@main
        id: testdriver
        with:
          prompt: |
            1. navigate to youtube.com in google chrome
            1. search for cat videos
            1. click the first one
```

### Tips on Prompting

The best way to write your prompt is to open an incognito window and perform the test acttions yourself. Write down each step you take.

1. Every step should be a single action
2. Steps are short and clear. The more information, the more likely TestDriver will be confused.
3. TestDriver works great with text, icons, shapes, and colors. It doesn't work as well with precise positioning (100px above, next to, etc).

## Test Results

TestDriver reports it's results within the GitHub actions interface.

<img src="https://github.com/dashcamio/testdriver-web/assets/318295/83185198-0550-42c5-ae3e-3734e5e1ddee" width="500">

Once you click `Details` you can view the AI-generated test summary and Dashcam results under `Summary`. Click "View Recording" or click on the thumbnail to launch the Dashcam interface.

<img src="https://github.com/dashcamio/testdriver-web/assets/318295/b90d6e20-9ff3-476f-8d78-223fa2f76385" width="500">

## Test Replay

### AI Logs

You may need to select `CLI` under `APP` to view the TestDriver AI logs (marked in yellow). You'll see your prompt is fed to the AI one step at a time. Whenever the `>` appears, that is input to the AI.

You'll see the AI execute code (marked in green) that it has generated to accomplish your task.

As you play the video, the logs will playback in real time. Past logs are 100% opacity and future logs are reduced opacity. You can click on any timestamp to navigate to the point in the video where those logs were produced.

<img src="https://github.com/dashcamio/testdriver-web/assets/318295/bc9f339e-949c-4a39-9314-14ddbbd356ae" width="500">

### Chrome Logs

The Chrome console logs and network requests recorded from the test are available under the "Chrome" tab.

<img src="https://github.com/dashcamio/testdriver-web/assets/318295/70d3e77c-342f-46cc-95c1-5765bc1fa993" width="500">

## Building your application for development

If you do not already have deploy previews from something like Vercel or Netlify, you may build your application for testing on the machine at run time. Note that TestDriver will clone the repository and branch from which it is run.

In order to build your application, modify [the `.testdriver/prerun.sh` script](https://github.com/dashcamio/testdriver-web/blob/main/.testdriver/prerun.sh) to include your build steps. Fore example, you may add `npm build` here.

Note that currently causing an exception within `prerun.sh` may cause the test to silently fail.

- [ ] TestDriver Model V2
- [ ] Interface updates
  - [ ] Auto-focus AI logs in Dashcam.io
- [ ] Test Reporting and Analyitcs Dashboard
