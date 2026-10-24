# ask.recipes

[![ask.recipes MCP connector](https://glama.ai/mcp/connectors/recipes.ask/ask-recipes/badges/score.svg)](https://glama.ai/mcp/connectors/recipes.ask/ask-recipes)
[![LobeHub listing](https://lobehub.com/badge/mcp/ask-recipes)](https://lobehub.com/mcp/ask-recipes)
Also on [Smithery](https://smithery.ai/servers/rcm7/ask-recipes).

Your AI's cookbook. A remote MCP server: connect it once and your agent finds recipes, checks nutrition, cooks from what is in the fridge, keeps your cookbooks and pantry, remembers what you cooked, keeps your own recipes and sends any of them to your Thermomix.

Free. No ads. Every recipe links to its source.

```
https://mcp.ask.recipes/mcp
```

Works with Claude, ChatGPT, Claude Code, Cursor and any MCP client that speaks streamable HTTP with OAuth.

## Connect

**ChatGPT**: open the [ask.recipes app page](https://chatgpt.com/plugins/plugin_asdk_app_6ad7e6161a3881918bd701a6a39bb49c) and add it. Manual route: Settings → Connectors → Advanced → Developer mode → add the URL, OAuth as the authentication.

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

**Anything else**: streamable HTTP, OAuth 2.1 with PKCE and dynamic client registration. Discovery at `https://mcp.ask.recipes/.well-known/oauth-protected-resource`.

Sign-in is an email address and the code sent to it. No password, no newsletter.

## What to ask

- "What's for dinner? Chicken thighs, a lemon and rice, under 40 minutes."
- "I have oats, milk, eggs and berries. Breakfast?"
- "A high-protein lunch under 500 calories."
- "Something vegetarian people actually rate well, 30 minutes."
- "Ten people coming over on Saturday. One pot."
- "The second one in full, for six." then "Save it under BBQ."
- "What's in my Stews cookbook?"
- "Bought rice, eggs and two chickens." then later "What can I make with what I have?"
- "We made the curry tonight, kids loved it." then later "What did we cook last week?"
- "Keep this family recipe: ..." or "Here's a photo of my mum's recipe card, keep it."
- "Give me a link to send my sister the lasagna I uploaded."
- "Send the lasagna to my Bimby."

## Tools

| tool | does |
|---|---|
| `search_recipes` | Search by dish or ingredient. Filters: total time, rating, review count, diet (vegetarian, vegan, gluten-free, dairy-free, nut-free), calories, protein, fat, carbs, sugar, fiber, ingredients to leave out, head count. |
| `find_by_ingredients` | Rank recipes by how many of your ingredients they use and how few extra they need. Your pantry counts as on hand; with nothing passed it cooks from the pantry alone. |
| `get_recipe` | One recipe in full: ingredients, steps, times, yield, nutrition, source link. Scales the ingredients to a servings number. |
| `get_pantry`, `add_to_pantry`, `remove_from_pantry` | What is in your kitchen, kept by talking: "bought milk and onions", "used the last eggs". |
| `save_recipe`, `unsave_recipe`, `list_saved` | Your collection, kept in cookbooks, with a note per recipe and when you last cooked it. Kept across sessions and clients. |
| `list_cookbooks`, `create_cookbook`, `update_cookbook`, `delete_cookbook` | Named cookbooks ("Stews", "BBQ", "Christmas"), created on first use. Deleting one never loses a recipe. |
| `mark_cooked`, `cooked_history` | A cooking diary kept by talking: what you cooked, when, and how it went. Your agent reads it before planning a week so nothing repeats. |
| `upload_recipe` | A private recipe of your own: typed, dictated, from a photo, or extracted from a web page. |
| `share_recipe` | An unlisted link to one of your uploaded recipes, readable without an account. |
| `connect_cookidoo`, `disconnect_cookidoo` | Link your Cookidoo account (Thermomix / Bimby) through a one-time form. |
| `send_to_thermomix` | Any recipe into your Cookidoo as a private created recipe, with time, temperature and speed on every step, ready for guided cooking. |
| `list_cookidoo_recipes`, `search_cookidoo`, `import_cookidoo_recipe` | Your own Cookidoo recipes, Cookidoo's catalogue through your account, and a copy of one into your private collection. |

## Good to know

- Search ranks by how many people rated a recipe and applies no rating cut on its own. Ask for well-rated only and your agent passes a minimum.
- Nutrition is per serving as the source published it. Nutrition filters only return recipes whose yield is stated in servings.
- "Not chicken again": your agent can leave ingredients out of one search, matched as whole words, so "egg" never drops eggplant and "nut" never drops nutmeg or coconut.
- From six people up, dishes cooked in one vessel (stews, braises, soups, casseroles, tray bakes, roasts) rank ahead of dishes cooked per portion, and your agent can leave the per-portion ones out.
- Diet flags are judged from the ingredient list, conservatively: oats count as gluten, peanuts count as nuts, coconut does not. A recipe on the edge is left out of a diet filter rather than let in.
- Share links carry schema.org Recipe markup with the nutrition, so a shared recipe imports by URL into MyFitnessPal, Cronometer, Paprika and most recipe apps. Crawled recipes cannot be shared this way; share the source link instead.
- Cookidoo is an unofficial integration; Vorwerk offers no API. The Cookidoo tools work in Claude and other MCP clients and are not available in ChatGPT. Recipes imported from Cookidoo stay private and are never shareable.
- The corpus is built from openly licensed recipe data and recipe sites' own schema.org markup. Crawling is done by [AskRecipesBot](https://ask.recipes/bot): honest user agent, robots.txt respected, one request at a time per site.
- No browsing UI exists and none is planned. The agent is the interface.

## Links

[ask.recipes](https://ask.recipes) · [Docs](https://ask.recipes/docs) · [Privacy](https://ask.recipes/privacy) · [Terms](https://ask.recipes/terms) · hello@ask.recipes

Built by [Ricardo](https://x.com/RCM7). The server is not open source; this repository exists so the connector is easy to find.
