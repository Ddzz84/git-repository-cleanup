# git-repository-cleanup
reduce repository size

# create tag where you start new branch
BRANCH_START=master
BEGIN_INIT_TAG=new_init_tag 

git checkout --orphan=$BEGIN_INIT_TAG
git commit -m "new init"

# restore all commit

LAST_COUNT=$(git rev-list $BRANCH_START new_init..HEAD --count)
for commit in $(git log $BRANCH_START --reverse  -n $(expr $LAST_COUNT - 1)  --pretty=%H) 
do 
	git cherry-pick $commit
done
