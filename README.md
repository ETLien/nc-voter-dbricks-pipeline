# NC Voter Data Pipeline (Azure Databricks)

An automated pipeline that tracks weekly-updated North Carolina voter registration
and voter history data (published by the NC State Board of Elections), detects
when new data is available, and processes it for downstream use.

## Background

This is a refactor of [an earlier version of this project](https://github.com/ETLien/nc-voter-pipeline),
originally written while I was still learning Python. The original still works,
but it became increasingly harder to follow as I extended it incrementally over time rather than
restructuring it. This version rebuilds the same core logic as a
modular pipeline (partly to make it maintainable and partly to get hands-on
experience with Azure Databricks).

Data-specific details (source, update cadence, field meanings) are still
accurate in the [original README](https://github.com/ETLien/nc-voter-pipeline/blob/main/README.md). I'll try to avoid repeating details here.

## What it does

- Checks the source S3 for new files (now by comparing the ETag, I was initially doing this with Last-Modified).
- Downloads and unzips new files only when something has actually changed.
- Tracks pipeline state in a JSON file so runs are resumable from the right part of the pipeline if there is an interruption.

## Status

Currently working: file-change detection, download, unzip.
Next: validation checks, identifying new data, syncing to DB, cleanup.
