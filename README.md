# Microsoft 365 uBlock Whitelist

![Workflow Status](https://img.shields.io/github/actions/workflow/status/GruberMarkus/ublock-whitelist-m365/update-ublock.yml)
[![Last Commit](https://img.shields.io/github/last-commit/GruberMarkus/ublock-whitelist-m365)](https://github.com/GruberMarkus/ublock-whitelist-m365/commits/main)
[![License](https://img.shields.io/github/license/GruberMarkus/ublock-whitelist-m365)](https://github.com/GruberMarkus/ublock-whitelist-m365/blob/main/LICENSE)
[![Repo Size](https://img.shields.io/github/repo-size/GruberMarkus/ublock-whitelist-m365)](https://github.com/GruberMarkus/ublock-whitelist-m365)
[![Stars](https://img.shields.io/github/stars/GruberMarkus/ublock-whitelist-m365?style=social)](https://github.com/GruberMarkus/ublock-whitelist-m365/stargazers)

---

## About

This repository automatically generates and maintains a **uBlock Origin whitelist filter list** containing all known Microsoft 365 (M365) service URLs.  
The generated list is updated every **5 hours** using a GitHub Actions workflow that pulls the official Microsoft 365 endpoint data and reformats it into a compatible uBlock Origin filter file.

## Features

- Fetches the official Microsoft 365 endpoints from Microsoft's [Office 365 IP Address and URL web service](https://endpoints.office.com/).
- Converts the domain list into uBlock Origin exception rules (`@@||domain^`).
- Updates automatically via cron schedule, so the list always stays up-to-date.
- Commits changes back into the repository for convenient subscription.

## Usage in uBlock Origin

1. Open the uBlock Origin **Dashboard** in your browser.
2. Go to the **Filter lists** tab.
3. Scroll to **Custom** and paste the raw list URL: `https://raw.githubusercontent.com/GruberMarkus/ublock-whitelist-m365/main/ublock-whitelist-m365.txt`
4. Click *Apply changes*.
5. The whitelist rules for M365 services will now be applied.

## Example Entry

The generated whitelist file looks like this:
```
! Title: Microsoft 365 URL Whitelist
! Version: 202510020835
! Filter list description: This filter list contains all known URLs for Microsoft 365 services, unblocking them in uBlock Origin.
! Expires: 24 hours
! Homepage: https://github.com/GruberMarkus/ublock-whitelist-m365
! Source: https://endpoints.office.com/endpoints/worldwide
! Last Updated: 2025-10-02T06:35:00Z

@@||office.com^
@@||teams.microsoft.com^
@@||outlook.office365.com^
...
```


## Automation Details

The workflow **Update M365 uBlock List** runs:
- On a schedule every 5 hours
- Or manually via workflow_dispatch

Steps performed:
- Generate unique GUID and fetch JSON endpoints from Microsoft.
- Parse URL domains using jq and format as `@@||domain^`.
- Write metadata headers for uBlock filtering.
- Commit and push updated list back into the repo.

## Repository Structure

- `ublock-whitelist-m365.txt`: The generated filter list for uBlock Origin.
- `.github/workflows/update-ublock.yml`: GitHub Actions workflow that runs the automation.

---






