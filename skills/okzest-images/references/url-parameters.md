## How personalisation works

- A text layer whose text contains `[layer_id]`, the layer's own ID in square brackets, is dynamic.
- The URL parameter with that name replaces the bracketed text. `default_text` shows when no value is given.
- Text without its own bracketed ID is static.
- An image layer has an `image_url`, which is the default image. A URL parameter named after the layer swaps it for another image. The image is resized to the layer's width and keeps its aspect ratio.
- Layers draw in order, so later layers sit on top.

Example: a text layer with `layer_id` `first_name` and text `Hi [first_name]!` shows "Hi there!" by default, and `{"first_name":"Jane"}` makes it "Hi Jane!".
