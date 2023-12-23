# [Taskwarrior](https://taskwarrior.org/) ⬄ [Google Tasks](https://support.google.com/tasks/answer/7675772?hl=en&co=GENIE.Platform%3DDesktop)

## Description

Given all tasks in your Google Task task list of a
taskwarrior _filter_ (combination of tags and projects) synchronise all the
addition/modification/deletion tasks between them.

## Demo - populating a list in Google Tasks (view from Google Calendar)

![demo_gif](misc/tw_gtasks_sync.gif)

## Motivation

While Taskwarrior is an excellent tool when it comes to keeping TODO lists,
keeping track of project goals etc., lacks the portability, simplicity and
minimalistic design of Google Calendar. The latter also has the following
advantages:

- Automatic sync across all your devices
- Comfortable addition/modification of events using voice commands
- Actual reminding of events with a variety of mechanisms

## Override Calendar API key

Unfortunately I've yet to verify this app with Google so new users are
currently blocked from using it. To bypass that you can register for your own
developer account with the Google Calendar API with the following steps:

Firstly, removed the `~/.gtasks_credentials.pickle` file on your system since that
will be reused if found by the app.

For creating your own Google Developer App:

- Go to the Google developer console
- Make a new project
- From the sidebar go to `API & Services` and once there click the `ENABLE APIS AND SERVICES` button
- Look for and Enable the `Tasks API`

Your newly created app now has access to the Tasks API. We now have to create
and download the credentials:

- Again, from the sidebar under `API And Services` click `Credentials`
- Enable the `Tasks API`
- On the sidebar click `Credentials`, and once there click `CREATE CREDENTIALS`
- Create a new `OAuth Client ID`. Set the type to `Desktop App` (app name is not
  important).
- Finally download the credentials in JSON form by clicking the download button
  as shown below. This is the file you need to point to when running
  `tw_gtasks_sync`.

  ![download-btn](misc/gcal-json-btn.png)

To specify your custom credentials JSON file use the `--google-secret` flag as follows:

```sh
tw_gtasks_sync -l "<list-name>" -t "<taskwarrior-tag>" --google-secret "<path/to/downloaded/json/file>"
```

## Usage Examples

Run the `tw_gtasks_sync` to synchronise the Google Tasks list of your choice with
the selected Taskwarrior tag(s). Run with `--help` for the list of options.

```sh
# Sync the +remindme Taskwarrior tag with the Google Tasks list named "TW Reminders"

tw_gtasks_sync --help
tw_gtasks_sync -t remindme -l "TW Reminders"
```

## Installation

### Package Installation

Install the `syncall` package from PyPI, enabling the `google` and `tw`
extras:

```sh
pip3 install syncall[google,tw]
```

## FAQ

### How do I mark an item as done from Google Tasks

Simply mark them as completed.
