---
name: okzest-images
description: Make personalised images from templates with OKZest - email headers with a first name, social quote cards, certificates, and one image URL per recipient for a mail merge. Use when the user wants a templated or personalised image, or an image URL for an email or automation. Not for free-form illustration or photos.
---

# OKZest images

OKZest turns a template into an image. You design a template once, mark the parts that change, and OKZest generates a personalised image from a URL. This skill covers the OKZest tools: how to set up a template and how to get a URL for each person.

## When to use this

Use it when the user wants:

- an email header or banner that shows each recipient's name, photo or offer
- a social card, quote card, certificate or OG image built from a template
- an image URL they can paste into an email, a page or an automation
- the same image in many versions, one per recipient

Do not use it for:

- illustrations, artwork or photos made from a description
- editing or restyling an existing photo

OKZest is a template tool, not an AI image generator. It places text and images you supply onto a canvas. It does not invent pictures. If the user asks for something it cannot do, say so and stop.

## Setup check

Before anything else, check that the OKZest tools are available (`list_designs`, `list_projects`, `create_design` and so on). If they are not, tell the user two steps:

1. Get an API key at Settings, then API Keys, in your OKZest account. No account yet: https://okzest.com/?utm_source=claude-skill&utm_medium=plugin&utm_campaign=okz337
2. Enter the key when Claude Code asks for it, or reconfigure the plugin in `/plugin`.

Never ask the user to paste the key into chat.

The Free plan is badged. Images from a Free plan account carry a small "Made with OKZest" badge, and the Free allowance is 500 images; after that they stop showing until the account upgrades. Do not promise clean or unbranded output on a Free key. Check the plan details at https://okzest.com/pricing before promising anything else.

## The workflow

1. If the account has more than one project, call `list_projects` and ask which one to use.
2. Call `list_designs` to see whether a suitable template already exists. Reuse it rather than creating a new one.
3. Call `list_fonts` with a search term, for example `roboto`. Pass `projectId` when the account has several projects, because uploaded fonts belong to one project and are hidden without it. At most 100 fonts come back, so narrow the search if `total_count` is higher. Use the `font_family` exactly as returned; for an uploaded font it differs from the label.
4. Call `create_design` with a canvas size, a background colour and the layers. It saves the template as a JPEG design and returns its render URL, its URL parameters and a preview image URL that only works for a short time.
5. Call `generate_image_url` with the design ID and a `urlParams` object for each recipient. It returns a URL and saves no files; the image is generated when the URL is opened.
6. Open the URL and look at the result before telling the user it is done. Do not assume what it looks like.

Use `modify_design_layers` only for a one-off preview. Without a format it returns a JPEG (PNG when the background is transparent); you can ask for `jpeg`, `png` or `webp`. Its URL is temporary, so never put it in an email or any permanent page.

## How personalisation works

- A text layer whose text contains `[layer_id]`, the layer's own ID in square brackets, is dynamic.
- The URL parameter with that name replaces the bracketed text. `default_text` shows when no value is given.
- Text without its own bracketed ID is static.
- An image layer has an `image_url`, which is the default image. A URL parameter named after the layer swaps it for another image. The image is resized to the layer's width and keeps its aspect ratio.
- Layers draw in order, so later layers sit on top.

Example: a text layer with `layer_id` `first_name` and text `Hi [first_name]!` shows "Hi there!" by default, and `{"first_name":"Jane"}` makes it "Hi Jane!".

## Worked examples

### 1. Email header with a first name and a photo

Prompt the user might give: "Make a welcome email header for Jane with her photo."

What to do: list designs first and reuse a header if there is one. Otherwise create a 600 by 200 design with a text layer `first_name` reading `Hi [first_name]!` (default `there`) and an image layer `photo` with a default image. Then call `generate_image_url` with `{"first_name":"Jane","photo":"<her photo URL>"}` and open the result.

```json
[
  {"layer_id":"first_name","type":"text","text":"Hi [first_name]!","default_text":"there","x":220,"y":70,"width":360,"font_size":40,"color":"#111111"},
  {"layer_id":"photo","type":"image","image_url":"https://example.com/default-photo.jpg","x":20,"y":20,"width":160,"height":160}
]
```

### 2. Social quote card

Prompt the user might give: "Make a quote card for this line, in our brand colours."

What to do: ask for the quote, the author and the hex colours. Search `list_fonts` for a font the user names, or ask. Create a square design with a background colour and two text layers, `quote` and `author`, each with its own ID in brackets. Use `generate_image_url` for each new quote, so the same template serves every card.

```json
[
  {"layer_id":"quote","type":"text","text":"[quote]","default_text":"Your quote here","x":60,"y":120,"width":960,"font_size":64,"color":"#ffffff"},
  {"layer_id":"author","type":"text","text":"[author]","default_text":"Author","x":60,"y":900,"width":960,"font_size":36,"color":"#ffffff"}
]
```

### 3. Mail-merge batch

Prompt the user might give: "Make versions of that header for Jane, Raj and Mei."

What to do: reuse the saved header from example 1. Call `generate_image_url` once per person, changing only `urlParams`. Return a list of name and URL pairs, and open at least one to check it. The user pastes each URL into their email platform's merge field for that recipient.

```json
{"first_name":"Raj","photo":"https://example.com/raj.jpg"}
```

## Common mistakes

- A `font_family` that did not come from `list_fonts`, or an uploaded font looked up without the right `projectId`.
- A bracketed placeholder that does not match any layer's own `layer_id`.
- Using the temporary `modify_design_layers` URL in a sent email.
- A background photo that is not the first layer, so it covers the text.
- A canvas size outside the allowed range. Width and height must each be between 1 and the maximum `create_design` states.
- Asking the user to paste the API key into chat.
- Saying an image is ready without opening its URL.

## Limits

OKZest places your text and images on a canvas. It does not write copy, create pictures or retouch photos. Only claim what the tools above do. If the user needs something else, say so plainly.
