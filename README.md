# PostgreSQL Repository Fix Buildpack

This buildpack fixes the PostgreSQL repository issue for Ubuntu Focal (20.04) deployments on Heroku/Dokku.

## Problem

As of July 31, 2025, Ubuntu Focal (20.04) was removed from the primary PostgreSQL APT repository (apt.postgresql.org) and moved to the archive mirror. This causes buildpacks to fail with:

```
E: The repository 'http://apt.postgresql.org/pub/repos/apt focal-pgdg Release' no longer has a Release file.
```

## Solution

This buildpack runs before the apt buildpack and:

1. Imports the PostgreSQL GPG key
2. Configures the archive repository for Ubuntu Focal
3. Clears stale package lists

## Usage

Add this buildpack before the apt buildpack in your `.buildpacks` file:

```
https://github.com/your-username/postgresql-fix-buildpack.git
https://github.com/heroku/heroku-buildpack-apt.git
```

## Files

- `bin/detect` - Detects if this buildpack should be used
- `bin/compile` - Runs the PostgreSQL repository fix
- `bin/release` - Release script (empty for this buildpack)

## Installation

1. Clone this repository
2. Push to your GitHub account
3. Reference in your `.buildpacks` file

## License

MIT