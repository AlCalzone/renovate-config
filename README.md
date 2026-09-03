# Renovate presets for AlCalzone

Shared [Renovate](https://docs.renovatebot.com/) configuration. Repositories reference it from `.github/renovate.json5`:

```json5
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>AlCalzone/renovate-config:library"]
}
```

| Preset | Use for |
|---|---|
| `default` | Base for everything. Monthly window on the 1st (Europe/Berlin), 7 day minimum release age, `rangeStrategy: bump`, automerge for devDependency patch/minor, dependency patch and GitHub Actions minor/patch. TypeScript minor/major wait for dashboard approval. |
| `library` | Published npm packages. No lockfile maintenance, since transitive dependencies are resolved by consumers. |
| `app` | Deployed applications. Adds one monthly lockfile maintenance PR. |

Per repository, add a rule that keeps `@types/node` on the major matching `engines.node`, since Renovate does not derive it:

```json5
"packageRules": [
  // Raise together with engines.node
  { "matchPackageNames": ["@types/node"], "allowedVersions": "<21" }
]
```
