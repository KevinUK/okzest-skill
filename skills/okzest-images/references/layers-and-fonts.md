## Layers and fonts

Call `list_fonts` with a search term, for example `roboto`. Pass `projectId` when the account has several projects, because uploaded fonts belong to one project and are hidden without it. At most 100 fonts come back, so narrow the search if `total_count` is higher. Use the `font_family` exactly as returned; for an uploaded font it differs from the label.

- An image layer has an `image_url`, which is the default image. A URL parameter named after the layer swaps it for another image. The image is resized to the layer's width and keeps its aspect ratio.
- Layers draw in order, so later layers sit on top.
