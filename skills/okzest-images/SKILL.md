---
name: okzest-images
description: Use when the user wants a personalised or templated image (email header with a first name, social card, certificate, banner, OG image) or an image URL for an email or automation, using OKZest. Not for free-form illustration or photo generation.
---

# OKZest images

> STUB: placeholder structure. Final copy comes from OKZ-605 (Jake) and is fact-checked by Guinan.

OKZest is a template tool, not an AI image generator. Use it to render designs with per-recipient text and images.

## Setup check

If the OKZest tools are missing, tell the user to create an API key at Settings, API Keys on okzest.com and set `OKZEST_API_KEY`. Sign-up link: https://okzest.com/?utm_source=claude-skill&utm_medium=plugin&utm_campaign=okz337. Never ask the user to paste the key into chat.

## Workflow

1. `list_projects` if the account has more than one project.
2. `list_designs` to reuse an existing design.
3. `list_fonts` (with `projectId` for several projects) before choosing a `font_family`.
4. `create_design`, then `generate_image_url` with `urlParams` for each recipient.
5. Use `modify_design_layers` only for one-off previews, because its URL expires.

See `references/` for detail.
