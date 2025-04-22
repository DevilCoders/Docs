## Motivation
To deploy something we need to describe two pieces of a puzzle:
 * artifacts and configuration settings.
 Files, command line arguments, env variables, etc.
 * subsets of nodes.
 Where we want particular variant of our **unit** to be deployed.

Unfortunately these two items are often intertwined, e.g.
>I want to enable this feature on `yt-hahn` hosts, but I want other settings to be "inherited" from
>whatever wider variant this is (e.g `DEBUG` logging level in my service).

That is why we call them _vyshivankas_. 

**What if** we could describe unit variants **and** deployment scheme:
  * in one place
  * without making a mess again

🤔🤔🤔


## Unit
We have units of deployment, e.g. `PortoDaemon` (later will come `PackageUnit`, `SystemDaemon`).
All these objects have two sections that can fully describe them:
  * `ObjectMeta` - meta data like user defined version, name, etc.
  * `{Unit}Spec` - specific description what to perform on host

Specification contents fully define what will be applied on host. No other variables can affect that. I.e
`spec` does not depend on external variables, files, etc.

User tasks is to come up with a scheme which can **generate** unit description tailored for specific host.
How can one achieve that? We can use Jinja or custom generators **AND** a scheme to choose particular
 spec on host as we do not have external orchestrator (and may be we will not).

### Variants
Quick question: how one chooses which variant of spec to be applied on a host? 
We use host information! I.e `variant = f(host_info)`. And if `host_info` changes - 
new variant may be chosen for host. This can look like:
```python
if walle_project in ['yt-hahn-nodes', 'yt-arnold-nodes']:
    variant = '2.0-1725373-yt'
elif geo == 'sas':
    variant = '2.0-1762927-sas'
else:
    variant = '2.0-1762927-stable'
```
Seems legit. But!
In real life we may end up with variants like `2.0-126352-sas-stable-debug-log-no-htb`. And how
could we generate such variants? We'd use same logic in our generator
```python
variants = []
for loglevel in ['DEBUG', 'INFO']:
  for server in ['sas.hbf.yandex.net', 'man.hbf.yandex.net', 'vla.hbf.yandex.net']:
     variants.append(generate_variant(loglevel, server))
```
And this is not perfect:
  * Duplication of logic in two very separate places. Or combinatorial explosion.
  * Cognitive load to come up with names for variants.
  * We need this generator.
  * We need types and current approaches (Jinja) operate on byte level. I.e string manipulation.

What if there is another way?
