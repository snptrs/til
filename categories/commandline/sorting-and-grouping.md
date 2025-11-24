# Sorting and grouping a list of values

Occasionally I need to randomise and group a list of values. I usually handle the steps separately, often using whatever randomiser I find online as the easiest option. But this is the kind of thing that lots of unix utilities are perfect for, so I explored a few different options for doing this on the command line.

## Input data

Let’s use this list of names as the input data:

```text:names.txt
Jerome
Jane
Sydney
Joshuah
Yvette
Merl
Mariano
```

## Sorting randomly

`sort -R` and `shuf` will both randomly sort a list. It seems that `shuf` is more efficient though,[^1][^2] so we may as well use that.

```bash
shuf names.txt
```

## Grouping

Most things can be done with `awk`, but I just find its syntax so impenetrable, I try to avoid it if at all possible. Out of interest, this is as close as I got to grouping the names into threes. It seems to work, but if I wanted to change this in the future I know I’d have to spend ages trawling through docs to figure it out.

```bash
awk '{printf "%s%s", (NR%3==1 ? "" : ", "), $0} NR%3==0{print ""} END{if(NR%3!=0) print ""}' names.txt
```

The `paste` utility is a much simpler option in this instance. It just merges lines, joining them with a tab by default, or an optional list of `-d|--delimiters`. Use `-` to read from stdin, reading one line at a time for each instance of `-`.

This is what I ended up with to group in threes, separated with a comma:

```bash
paste -d , - - -
```

## Putting it all together

This will take the list of names, randomly sort them and output them as groups of three:

```bash
$ shuf names.txt | paste -d , - - -

Joshuah,Merl,Mariano
Jane,Yvette,Jerome
Sydney,,
```

We do end up with some trailing commas when there are too few values to complete the group. I’ll have to figure out a way to deal with that.

[^1]: https://nickjanetakis.com/blog/randomly-order-lines-on-the-command-line-with-sort-or-shuf
[^2]: https://stackoverflow.com/questions/14727151/fastest-way-to-shuffle-lines-in-a-file-in-linux