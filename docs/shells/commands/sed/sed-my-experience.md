Once upon a time I found this page:
<http://sethrobertson.github.io/GitBestPractices/>
from this [repo](https://github.com/SethRobertson/GitBestPractices).

## Initial file

I downloaded it from the repo's `gh-pages` [branch](https://raw.githubusercontent.com/SethRobertson/GitBestPractices/gh-pages/index.md) and saved as `git-best-initial.md`

After grabbing via Web Clipper (Chrome browser plugin), this file needed to be edited. The **Table of Content** links in this file do not work correctly, and some code blocks look ugly.

## Edit with `sed` & Regular Expressions

Initially I was processing the file along with the TOC (Table Of Content):

```
cat git-best-initial.md | sed -e 's/ \/>/><\/a>/g' -e 's/\* \(\w.*$\)/\* **\1**/g' -e 's/^    //g' -e 's/^### /### \&emsp; /g' | less
```

But then I deleted the TOC because it is automatically generated by Docusaurus (from the h2 & h3 headers) and simplified the code a bit:

```
cat git-best-initial.md | sed -e 's/\*   \(.*$\)/\* **\1**/g' -e 's/^### /### \&emsp; /g' > result.md
```

## Resulting file

Finally I manually edited the resulting file and got this:

[Git Best Practices](../../../workplace/git/git-best-practicies)
