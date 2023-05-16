# Better RSpec output formatting

The default RSpec output just shows a series of green dots for tests that pass, and a red F for tests that fail.

It’s possible to get more helpful output showing the `describe`, `context` and `it` strings so you can easily see what’s passing and failing.

![Screenshot of terminal showing RSpec output](../../../assets/rspec-with-document-formatting.png)

Either pass `--format documentation` as a command line option when running RSpec, or include it in your project’s .rspec file. You can also use `-fd` as a shorter version.

I’ve seen lots of recommendations to also pass `--color` (or `-c`) to colourise the output, but it’s always been in colour for me anyway so I don’t add that. It may be dependent on your terminal or shell setup though.

There are some other [formatting options](https://rspec.info/documentation/3.12/rspec-core/RSpec/Core/Formatters.html) which I haven’t used yet.