# git-tags
A repo to test the git tags usage



**Objective**: 
* see how git tags works. What happens when you delete the branch that had the published commit tag?

**Steps**:
* read docs about `git tag` (otherwise, you'll be lost :) ) ✅
* create a branch from master ✅
* add changes to the new branch ✅
* create a tag within the branch ✅
* publish the tag ✅
* create a PR against master and merge it ✅
* delete the branch ✅
* go to the `new-branch` tag and see if you can get the data ✅


**Results**
Even after deleting the branch, the tag is available (which is awesome!)
* v1.0.0 has the initial steps
* v1.1.0 has the initial steps + the check marks for those steps that were completed (at that time)
* v1.2.0 has all the changes from v1.1.0 + the changes introduced at `master` (with extra steps and a new file!)

**About git tags**
Check the awesome post from Kolosek: https://dev.to/neshaz/a-tutorial-for-tagging-releases-in-git-147e or you can use [this link](about-tags.md).
