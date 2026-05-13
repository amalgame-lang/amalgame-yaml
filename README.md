# amalgame-yaml

Pure-Amalgame YAML 1.2 subset reader for [Amalgame](https://github.com/amalgame-lang/Amalgame).
Block mappings, block sequences, scalars (bool/int/float/string),
single- and double-quoted strings, comments — the shape a CI / app
config typically uses.

Originally bundled in amc's `src/stdlib/yaml.am`; extracted into
this external package as part of the framework split (post-v0.7.5).

## Install

```bash
amc package add yaml                  # via the curated index
amc package add github.com/amalgame-lang/amalgame-yaml@v0.1.0
```

Requires **amc 0.7.7+**.

## Surface

```amalgame
import Amalgame.Collections
import Amalgame.Formats.Yaml

class Program {
    public static void Main() {
        let src: string = "name: amalgame\nversion: 0.7.7\nfeatures:\n  - pkg-mgr\n  - lsp\n"
        let root: YamlValue = Yaml.Parse(src)

        let name: YamlValue = root.Get("name")
        Console.WriteLine(name.AsString())          // → amalgame

        let feats: YamlValue = root.Get("features")
        let n: int = feats.Length()
        Console.WriteLine(String_FromInt(n))        // → 2
    }
}
```

Out of scope (parser raises an error or falls back to plain
string): anchors / aliases (`&anchor`, `*ref`), multi-doc
separators (`---` / `...`), flow style (`[1, 2]`, `{a: b}`),
multiline scalars (folded `>`, literal `|`), tags (`!!str`).

## Tests

```bash
./tests/run_tests.sh /path/to/amc
```

## License

Apache-2.0 — see `LICENSE`. No vendored third-party code.
