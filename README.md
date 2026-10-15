# ask.recipes

[![ask.recipes MCP connector](https://glama.ai/mcp/connectors/recipes.ask/ask-recipes/badges/score.svg)](https://glama.ai/mcp/connectors/recipes.ask/ask-recipes)
[![smithery badge](https://smithery.ai/badge/rcm7/ask-recipes)](https://smithery.ai/servers/rcm7/ask-recipes)

Your AI's cookbook. A remote MCP server: connect it once and your agent finds recipes, checks nutrition, matches what is in the fridge, saves your favourites and keeps your own recipes.

Free. No ads. Every recipe links to its source.

```
https://mcp.ask.recipes/mcp
```

Works with Claude, ChatGPT, Claude Code, Cursor and any MCP client that speaks streamable HTTP with OAuth.

## Connect

**Claude** (web, desktop, mobile): Settings → Connectors → Add custom connector → paste the URL above. Enable it in a conversation and sign in when asked.

**Claude Code**

```sh
claude mcp add --transport http ask-recipes https://mcp.ask.recipes/mcp
```

then `/mcp` to sign in.

**Cursor**, `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "ask-recipes": { "url": "https://mcp.ask.recipes/mcp" }
  }
}
```

**ChatGPT**: Settings → Connectors → Advanced → Developer mode → add the URL, OAuth as the authentication.

**Anything else**: streamable HTTP, OAuth 2.1 with PKCE and dynamic client registration. Discovery at `https://mcp.ask.recipes/.well-known/oauth-protected-resource`.

Sign-in is an email and a link. No password, no newsletter.

## What to ask

- "What's for dinner? Chicken thighs, a lemon and rice, under 40 minutes."
- "I have oats, milk, eggs and berries. Breakfast?"
- "A high-protein lunch under 500 calories."
- "Something vegetarian people actually rate well, 30 minutes."
- "The second one in full." then "Save it."
- "What did I save last week?"
- "Keep this family recipe: ..." or "Here's a photo of my mum's recipe card, keep it."
- "Give me a link to send my sister the lasagna I uploaded."

## Tools

| tool | does |
|---|---|
| `search_recipes` | Search by dish or ingredient. Filters: total time, rating, review count, calories, protein, fat, carbs, sugar, fiber. |
| `find_by_ingredients` | Rank recipes by how many of your ingredients they use and how few extra they need. |
| `get_recipe` | One recipe in full: ingredients, steps, times, yield, nutrition, source link. |
| `save_recipe`, `list_saved` | Your collection, kept across sessions and clients. |
| `upload_recipe` | A private recipe of your own: typed, dictated, from a photo, or extracted from a web page. |
| `share_recipe` | An unlisted link to one of your uploaded recipes, readable without an account. |

## Good to know

- Search defaults to recipes rated at least 4.2 stars by at least 25 people. Ask your agent to loosen it for something obscure.
- Nutrition is per serving as the source published it.
- The corpus is built from openly licensed recipe data and recipe sites' own schema.org markup. Crawling is done by [AskRecipesBot](https://ask.recipes/bot): honest user agent, robots.txt respected, one request at a time per site.
- No browsing UI exists and none is planned. The agent is the interface.

## Links

[ask.recipes](https://ask.recipes) · [Docs](https://ask.recipes/docs) · [Privacy](https://ask.recipes/privacy) · [Terms](https://ask.recipes/terms) · hello@ask.recipes

Built by [Ricardo](https://x.com/RCM7). The server is not open source; this repository exists so the connector is easy to find.
