# mv_zettel.sh script

The `mv_zettel.sh` is a script in the repository that's available as a utility
to rename zettels.

```sh
./mv_zettel.sh <old-name-of-zettel> <new-name-of-zettel>
```

## Example

```sh
./mv_zettel.sh 4e7771c9.md linux-memory-zones
```

> It's optional to specify with or without the `.md` file extension for both the
> old and new zettel name. The script deals with it appropriately.

This will:

- Rename the file `4e7771c9.md` to `linux-memory-zones.md`

- Find all occurrences of `[[4e7771c9]]` among your zettels and
  replace them with `[[linux-memory-zones]]`

- Create a Git commit of **all** your changes.
