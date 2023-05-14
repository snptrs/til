# Better RSpec output formatting

The default RSpec output just shows a series of green dots for tests that pass, and a red F for tests that fail.

It’s possible to get more helpful output and see the `describe`, `context` and `it` strings.

![Screenshot of terminal showing RSpec output](../../../assets/rspec-with-document-formatting.png)

Either pass `--format documentation` as a command line option when running RSpec, or include it in your project’s .rspec file.

There are some other [formatting options](https://rspec.info/documentation/3.12/rspec-core/RSpec/Core/Formatters.html) which I haven’t used yet.