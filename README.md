[![Actions Status](https://github.com/raku-community-modules/Git-Log/actions/workflows/linux.yml/badge.svg)](https://github.com/raku-community-modules/Git-Log/actions) [![Actions Status](https://github.com/raku-community-modules/Git-Log/actions/workflows/macos.yml/badge.svg)](https://github.com/raku-community-modules/Git-Log/actions) [![Actions Status](https://github.com/raku-community-modules/Git-Log/actions/workflows/windows.yml/badge.svg)](https://github.com/raku-community-modules/Git-Log/actions)

NAME
====

Git::Log - Gets the git log as a Raku object

SYNOPSIS
========

Gets the git log as a Raku object

DESCRIPTION
===========

The first argument is the command line args wanted to be passed into `git log`. Optionally you can also get the files changes as well as the number of lines added or deleted.

Returns an array of hashes in the following format: `ID => "df0c229ad6ba293c67724379bcd3d55af6ea47a0", AuthorName => "Author's Name", AuthorEmail => "sample.email@not-a.url" ...`

If the option :get-changes is used (off by default) it will also add a 'changes' key in the following format: `changes => { $[ { filename => 'myfile.txt', added => 10, deleted => 5 }, ... ] }`

If there is a field that you need that is not offered, then you can supply an array, :@fields. Format is an array of pairs: `ID => '%H', AuthorName => '%an' ...` you can look for more [here](https://git-scm.com/docs/pretty-formats).

These are the default fields:

```raku
my @fields-default =
  ID          => '%H',
  AuthorName  => '%an',
  AuthorEmail => '%ae',
  AuthorDate  => '%aI',
  Subject     => '%s',
  Body        => '%b'
;
```

EXAMPLES
========

```raku
# Gets the git log for the specified repository,
# from versions 2018.06 to main
git-log(:path($path.IO), '2018.06..main')

# Gets the git log for the current directory, and does I<not> get the files
# changed in that commit
git-log(:!get-changes)
```

### sub git-log

```raku
sub git-log(
    *@args,
    :@fields = Code.new,
    IO::Path :$path,
    Bool:D :$get-changes = Bool::False,
    Bool:D :$date-time = Bool::False
) returns Mu
```

git-log's first argument is an array that is passed to C<git log> and optionally you can provide a path so a directory other than the current are used.

AUTHOR
======

Samantha McVey

Source can be located at: https://github.com/raku-community-modules/Git-Log . Comments and Pull Requests are welcome.

COPYRIGHT AND LICENSE
=====================

Copyright 2018 Samantha McVey

Copyright 2024 The Raku Community

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

