# personal-site

This is a simple Jekyll site.

## Local development (Apple Silicon / arm64)

Your error:

`LoadError: cannot load such file -- google/protobuf_c`

usually means Bundler installed **x86_64** native gems (like `google-protobuf`, `sass-embedded`, `ffi`) but you’re running **arm64** Ruby.

### Recommended fix: use a modern arm64 Ruby + install gems locally

- Install Ruby (pick one):
  - Homebrew Ruby (simple): `brew install ruby`
  - `rbenv` (recommended for projects): `brew install rbenv ruby-build`

- Ensure your shell is using the new Ruby (examples):
  - `which ruby`
  - `ruby -v`

Then from this repo:

```bash
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve
```

Or use the wrapper:

```bash
./bin/serve
```

### If you must stay on system Ruby (not recommended)

Force Bundler to build native gems for your current platform (requires Xcode Command Line Tools). This fixes both:

- `cannot load such file -- google/protobuf_c`
- `cannot load such file -- ffi_c`

```bash
bundle config set --local path vendor/bundle
bundle config set --local force_ruby_platform true
rm -rf vendor/bundle
bundle install
bundle exec jekyll serve
```

Or run:

```bash
./bin/setup
./bin/serve
```


