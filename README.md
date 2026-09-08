# scoop-lilbee

The [Scoop](https://scoop.sh) bucket for [lilbee](https://github.com/tobocop2/lilbee), the whole local AI stack in one executable.

```powershell
scoop install git
scoop bucket add lilbee https://github.com/tobocop2/scoop-lilbee
scoop install lilbee
```

`scoop update lilbee` upgrades. Scoop clones a bucket and updates it with `git pull`, so the manifests live here rather than in the lilbee source tree: your bucket stays three small files.

## What each manifest installs

| App | Build |
| --- | --- |
| `lilbee` | Reads your NVIDIA driver version and installs the matching CUDA build (555.85+ gets cu125, 551.61+ gets cu124), otherwise the Vulkan build. It says which one it picked. |
| `lilbee-cuda` | The cu125 build in one download. Needs driver 555.85+. |
| `lilbee-compat` | The pre-Haswell CPU build, for a machine without AVX2. |

Install only one of them: they all provide the `lilbee` command. To switch, `scoop uninstall` the current one first.

## Moved from the lilbee repository

This bucket used to live inside the lilbee repository. If you added it before 2026-09-08, your bucket points at the old location and cannot update. Re-add it:

```powershell
scoop bucket rm lilbee
scoop bucket add lilbee https://github.com/tobocop2/scoop-lilbee
```

That leaves your installed lilbee alone. It only replaces where Scoop reads manifests from.

## How the manifests stay current

lilbee's release pipeline pushes here, the same way it pushes the Homebrew tap. Its `scoop` job renders the version and hashes into these manifests, installs each one on a Windows runner, and pushes only if that install runs. Nothing here polls lilbee. Every version and hash is written by that job, so edit a manifest's shape, never its pins.

## License

[MIT](LICENSE), the same as lilbee.
