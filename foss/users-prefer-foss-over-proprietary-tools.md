---
date: 2021-01-18T18:35
tags: 
  - programming/inviting users to your project
  - programming/why is open source better
---

# Users prefer FOSS over proprietary tools, even at the cost of quality

"Proprietary is bad" / "Open source is good" - is a common heuristic. Though
what is it grounded in?

> [...] I think freedom is more important than technical progress. Proprietary
> software offers plenty of technical “progress”, but since I won’t surrender my
> freedom to use it, as far as I’m concerned it is no progress at all. [...]
>
> - Richard Stallman (author of GNU, Emacs, GCC, GPL, et.al), in
>   *Re: New maintainer* [Email thread] (2015), as quoted by Pereira in
>   *"The values of Emacs, the Neovim revolution, and the VSCode gorilla"*
>   [Blog post] (2021)[^pereira-2021]

Consider a user who is looking for a library to fit their needs. Said user finds
two projects, one being your free (as in freedom) and open source library, and
one other free (as in price) proprietary library. In most common of cases the
user will consider the two options carefully, comparing the feature sets, and
then still chose your options, even if it lacks in features.

Much of this comes from what Stallman talks about, there's also some other
factors.

## What the user considers

Pereira paints this quite black and white in his comment:

> Because of freedom, when faced with a question of using technology that is
>
> 1. Non-free, but objectively better
> 2. Free, but objectively worse
>
> the latter will always be picked. Given that most technological progress
> happens through the mechanisms of capitalism, “free” alternatives commonly
> lag behind to a large degree.
>
> (Pereira, 2021[^pereira-2021])

An (overly) extensive suite of features, versus "good enough" and free. Slow
and steady wins the race, and users knows this, even if it's just subconscious.

## It's safer to use FOSS

A user with a deep understanding of the open source world also understands that
it's usually safer to use an open source library. When it comes to security,
when a bug is found it is up to the community as a whole to look into it and
fix it. It's much more transparent and allows for anyone with the knowledge and
will to push a patch. If it's open source, the consensus is that there's more
eyes on its source and therefore less error-prone.

But there's another "safety" factor, and that's the fact that it's very hard to
kill a good open source project. Like a hydra, it will only multiply if someone
from the outside (ex: a company) is trying to kill it. Look at 
[youtube-dl](https://github.blog/2020-11-16-standing-up-for-developers-youtube-dl-is-back/)
for example. When DMCA put out a C&D order on the project, it was forked and
cloned to a stupid amount of other places, and in the end, GitHub took a stand
on the developers side. A good story with a happy end.
Something that never occurrs with proprietary products.

## Not to be confused with American freedom

The "FREEDOM"-fetish stereotype often associated with American culture (usually
in media and movies) is not to be considered the same as free and open source.

Don't let the Americans brag about freedom taint your look on freedom in
software. Seperate the two.

[^pereira-2021] Pereira, M. (2021, January 17). *The values of Emacs, the Neovim revolution, and the VSCode gorilla.* mpereia. <https://www.murilopereira.com/the-values-of-emacs-the-neovim-revolution-and-the-vscode-gorilla/> *(Found via Hacker News: <https://news.ycombinator.com/item?id=25810427>)*
