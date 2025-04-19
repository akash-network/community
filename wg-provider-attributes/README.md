---
title: "Provider Attributes Working Group"
date: 2023-1-10T00:19:20-08:00
description: This working group is for figuring out the schema for how providers specify attributes and for maintaining a list of required and optional provider attributes that can be referenced by Akash Network providers.

category: working-groups

meetings:
  dateLabel: Calendar
  link:
    label: Subscribe to Calendar
    link: "https://calendar.google.com/calendar/u/0?cid=Y18yNWU1ZTM3NDhlNGM0YWI3YTU1ZjQxZmJjNWViZWJjYzBhMDNiNDBmYjAyODc4NWYxNDE1OWJmYWViZWExMmUyQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20"

githubLink: "https://github.com/akash-network/community/tree/main/wg-provider-attributes"

discordLink: "https://discord.com/invite/akash"
---

# Akash Network Provider Attributes Working Group

This working group is for figuring out the schema for how providers specify attributes and for maintaining a list of required and optional provider attributes that can be referenced by Akash Network providers.

## Meetings

Joining the mailing list for the group will typically add invites for the following meetings to your calendar.

- Meeting 1 (e.g bug Scrub): \<weekday\> at \<time\> PT (Pacific Time) (every \<n\> weeks). Convert to your timezone (add link to https://dateful.com/time-zone-converter?t=09:00&tz=PT%20%28Pacific%20Time%29).

  - Meeting notes and Agenda.
  - Meeting recordings.

- Meeting 2: \<weekday\> at \<time\> PT (Pacific Time) (every \<n\> weeks). Convert to your timezone (add link to https://dateful.com/time-zone-converter?t=09:00&tz=PT%20%28Pacific%20Time%29).

  - Meeting notes and Agenda.
  - Meeting recordings.

- Regular WG Meeting: \<weekday\> at \<time\> PT (Pacific Time) (biweekly). Convert to your timezone (add link to https://dateful.com/time-zone-converter?t=09:00&tz=PT%20%28Pacific%20Time%29).

  - Meeting notes and Agenda.
  - Meeting recordings.

## Leads

- Maxime Beauchamp (@baktun14)

## Contacts

- @baktun14

## Goals

- Decide on provider attribute schema
- Document key attibutes including features, capabilities, hostname and location
- Figure out communication and roll out strategy to update existing providers
- Make code changes to provider code, clients and deployment code to enforce and use the attribute schema

## PRDs and other documentation

The implementation of the provider attribute schema currently resides here:

- https://github.com/ovrclk/cloudmos-config/blob/main/provider-attributes.md
- https://github.com/ovrclk/cloudmos-config/blob/main/provider-attributes.json

A form to use this schema has been implemented on Cloudmos in the providers section: https://deploy.cloudmos.io/providers

## Related SIGs

- sig-provider
- sig-clients
- sig-deployments
