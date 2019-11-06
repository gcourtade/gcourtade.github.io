---
layout: post
title:  GitHub Pages not working?
category: All 
comments: true
excerpt: This fix worked for me
---
Yesterday there was [an incident](https://www.githubstatus.com/incidents/42hkbtl63nmn) on GitHub Pages that caused the service to stop updating pages even after changes were committed.

Even after the incident was corrected, I could still not see changes to my site taking place. A quick fix that worked for me was to:
1. Go to `https://github.com/<username>/<repo>/settings`, and under **GitHub Pages** change the **Source** to **None**.
2. Make a small change to one of the files in the repo, commit and push the change.
3. Change the **Source** back to **master branch**, forcing GitHub Pages to update.