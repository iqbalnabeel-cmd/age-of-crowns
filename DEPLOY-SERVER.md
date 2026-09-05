# Putting the world server online

You only do this once. After that, every time you upload `worker.js` to the repo the server
updates itself, the same way GitHub Pages already updates the game.

You can do all of it from a phone.

## What you are uploading

Two files, both at the top level of the repo, same place as the game:

| File | What it is |
| --- | --- |
| `worker.js` | The whole server in one file. Built by `node build.mjs`. |
| `wrangler.toml` | Eleven lines telling Cloudflare what to run. |

## The six steps

1. **Upload both files to GitHub.** Same page you always use:
   https://github.com/iqbalnabeel-cmd/age-of-crowns/upload/main
   Drag them in, scroll to the bottom, **Commit directly to the main branch**, green button.

2. **Make a Cloudflare account** at https://dash.cloudflare.com/sign-up if you do not have one.
   Free. No card.

3. In the dashboard go to **Workers & Pages**, then **Create**, then the **Workers** tab, then
   **Import a repository**.

4. **Connect GitHub** and pick `iqbalnabeel-cmd/age-of-crowns`.
   Branch `main`. Leave the build command empty. Root directory `/`.

5. Press **Deploy**. It takes about a minute.

6. Cloudflare gives you an address like
   `https://age-of-crowns.<your-name>.workers.dev`
   **Send me that address** and I will bake it into the next build so nobody ever has to type it.

## Until then

The game asks for the address the first time you tap **Play online**, and remembers it on that
device. So you can test it the moment it is deployed, before I have baked it in.

## What it costs

Nothing, for anything you are likely to do. Cloudflare's free tier gives 100,000 requests a day
and Durable Objects are included. Each player asks the server for the world once every three
seconds while they have the game open, so one player watching for an hour is about 1,200 requests.
A world nobody has touched for three days stops advancing and stops costing anything at all.

## How to tell it is working

Open the address in a browser. You should see:

```
{"error":"Not found. The game itself is on GitHub Pages."}
```

That is the server saying hello. It only answers on `/api/...`, and the game does that for you.

## If something goes wrong

- **The deploy fails on `wrangler.toml`.** Check it uploaded to the top level of the repo, not
  inside a folder.
- **Play online says it cannot reach the server.** Check the address you pasted has no trailing
  slash and starts with `https://`.
- **A world code says "No such world".** Codes are per-server. A world made against one deployment
  does not exist on another.

## Running it here instead

For testing without deploying anything:

```
node tools/localserver.mjs 8787
```

That runs the same `worker.js`, providing the two things Cloudflare would: somewhere to keep
storage and something to call the alarm. `tools/v79-online.js` drives two real browsers against it.
