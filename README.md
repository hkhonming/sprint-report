# Sprint Report

This tool allows to generate a Markdown report of the issues completed within
a sprint in Jira

This command takes 2 parameters: the project Key and the name of the Sprint
The script will then print out the report on the default output and can easily
be redirected into a .md file

## Features
 - It will separate the issues by Type (Bug, Task, Storie)
 - It will create markdown link for Jira Key
 - If a bug summary includes LP#<bug id> it will substitute it for a link to the
   Launchpad bug
 - **Sprint Analytics**: Shows completed issues vs total issues in the sprint
 - **Story Points Analytics**: Shows completed story points vs total story points

## Usage

The tool supports three output modes:

### All (Default)
Print both the detailed task report and analytics:
```
$> sprint-report FR "2023 Pulse #1"
```

### Report Only
Print only the detailed task report (original behavior, no analytics):
```
$> sprint-report FR "2023 Pulse #1" --report-only
```

### Analytics Only
Print only sprint name and analytics (no detailed task breakdown):
```
$> sprint-report FR "2023 Pulse #1" --analytics-only
```

## Installation

Before installing this tool, ensure that you have installed the Jira pip
package:
```
$> pip install jira
```

## Configuration

The first time you run this command, you will be prompted for:
- The URL of your Jira instance
- Your email used for logging in
- Your Jira token (which can be found via https://id.atlassian.com/manage-profile/security/api-tokens)
- Your story points custom field ID (defaults to `customfield_10016` if not specified)

If saved, this information will be persisted in `~/.jira.token`

### Finding Your Story Points Field ID

Different Jira instances may use different custom field IDs for story points. To find yours:
1. Open a Jira issue that has story points set
2. View the issue in your browser and add `.json` to the URL (e.g., `https://your-jira.com/rest/api/2/issue/PROJ-123`)
3. Search for "story" in the JSON response to find the field name (e.g., `customfield_XXXXX`)
4. Use this field ID when prompted during setup

You can also manually edit the `~/.jira.token` file to update the `story-points-field` value.
