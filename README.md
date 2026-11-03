# OKZest for Claude

Design one template, then get a personalised image URL for each recipient, straight from Claude.

This plugin adds the OKZest skill and connects Claude to the OKZest tools. Ask for an email header with a first name, a social quote card, or one image per person on a mailing list, and Claude builds the template and gives you the image URLs.

OKZest is a template tool, not an AI image generator. It places the text and images you give it onto a canvas. It does not make pictures from a description, so use it for the images you need in many versions, not for artwork.

## What you can ask for

- "Make a welcome email header for Jane with her photo."
- "Make a quote card for this line in our brand colours."
- "Make versions of that header for Jane, Raj and Mei."

## Install

You need Claude Code and an OKZest account. No account yet: [sign up at okzest.com](https://okzest.com/?utm_source=claude-skill&utm_medium=plugin&utm_campaign=okz337).

```
claude plugin marketplace add KevinUK/okzest-skill
claude plugin install okzest@okzest
```

Get an API key at Settings, then API Keys, in your OKZest account. Claude Code asks for it (masked) when the plugin is enabled. To change it later, reconfigure the plugin in `/plugin`. Keep the key out of chat.

Then ask for an image.

If the OKZest tools do not appear, add the connection by hand. The endpoint is `https://api.okzest.com/mcp` and the key goes in the `x-api-key` header.

## Good to know

- **Fonts.** Claude picks fonts from the OKZest font list. Uploaded fonts belong to one project, so on an account with several projects Claude needs to know which one.
- **Format.** Previews come back as JPEG by default (PNG when the background is transparent). You can ask for PNG or WebP.
- **Preview links expire.** A preview URL works for a short time. The image URL for a saved template does not, so use that one in emails.
- **The Free plan is badged.** Images from a Free plan account carry a small "Made with OKZest" badge, and the Free allowance is 500 images; after that they stop showing until the account upgrades. See [okzest.com/pricing](https://okzest.com/pricing) for plan details.
- **Also have OKZest in claude.ai?** Claude Code treats the plugin and the claude.ai OKZest connector as the same server. If the connector is switched on but not authorised, neither one loads and you get no OKZest tools. Authorise the connector or switch it off in your claude.ai connector settings, then restart Claude Code.

## Links

- OKZest: https://okzest.com
- Docs: https://docs.okzest.com

## Licence

See `LICENSE`.
