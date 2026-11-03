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
