# Assets
Various assets of use within the network.  Intended strictly for my personal use.

## Castles

I use castles from _A Song of Ice and Fire_ as project codenames.  For instance, **Hellholt**
is the name for my Homelab project and general shared infrastructure, etc.  My domain name
there is `hellholt.net`.  I have separate email addresses under that domain.  Etc etc etc.

So when I want to start a new project, I can assign it a new name taken from a castle.

### Examples

```bash
# List the castle names that I've used as names for projects.
🦑nathan@Greyjoy:~/Projects/assets
$ jq '. | with_entries( select(.value.used) )' castles.json

{
  "Hellholt": {
    "used": true,
    "project_url": "https://github.com/hellholt/"
  },
  ...
}
```

```bash
# List the castle names that I've _not_ used as names for projects.
🦑nathan@Greyjoy:~/Projects/assets
$ jq '. | with_entries( select(.value.used | not) )' castles.json

{
  "Acorn Hall": {
    "used": false,
    "project_url": ""
  },
  ...
}
```

```bash
# Get a random unused castle name.
🦑nathan@Greyjoy:~/Projects/assets
$ jq --argjson castle_random $RANDOM -r '
  . 
  | with_entries( select(.value.used | not) )
  | keys 
  | .[$castle_random % length]
' castles.json
Hammerhal
```