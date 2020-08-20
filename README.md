Branching Flow:
---------------
Ref: [Github Flow](https://guides.github.com/introduction/flow/)
*Note: Follow releases in queue fashion*

**Mainline ( Infinite timeline branch ):**
`HEAD -> Master`

**Branches Naming convention:**
- *feature/*`<any-identifier>`
- *hotfix/*`<any-identifier>`
- *release/*`v<major-minor-patch>` ( semantic versioning system)

**Conventional Steps:**

1. Mainlain branch is single branch MASTER.
	```git
        git checkout -b feature/* master
    ```
2. Cut **feature/hotfix** from **MASTER** choose prefex based on need. Prefix will help in wildcard automation of CI solutions whether it may git actions or travis or jenkis.
3. Daily pull from *MASTER* to *LOCAL* stay upto date.
4. Automation steps
5. Feature is merged to **MASTER** after **unit test, CI, pull request**


**Automation Steps structure**:
- Branch name: `feature/notify-room-owner`
1. Developer commits to **feature/notify-room-owner**
2. Pushes to his code own branch ( **Daily/EOD commits** )
3. Github actions runs on commit action with prefix identification `feature/.*`
4. Runs `Unit Test` -> `auto send Coverage analysis report to SonarQube server`
5. `Unit Test` -> `PASS` -> Non-default-staging deployment. ( Hopefuly, it won't interrupt other developers staging or current default staging environment )
6. CI creates `auto pull` request from `feature/.*` to `MASTER` or can be `manual` to start with.
7. Black box testing commences ( Manual )
8. Upon accepting pull Request to `MASTER` and merge it.
    ```git
    $ git checkout master
    Switched to branch 'master'
    $ git merge --no-ff feature/<branch-name>
    $ git branch -d feature/<branch-name>
    Deleting 'feature branch` in remote.
    $ git push origin master
    
    ```
    ![](https://nvie.com/img/merge-without-ff@2x.png)
9. Deploy to `production` with a tag `v<major>.<minor>.<patch>` 


**Future Steps:**
- 6. Should be enhanced to `auto pull` from CI.
- 9. Auto tagging from `merge` event on github actions.
- 9. Auto deployment to `production` as a outcome of `successful merge` to `master` with CI.


**Some related articles and github actions:**

[Actions Auto tag](https://github.com/marketplace/actions/github-tag-bump)

[Github Flow](https://guides.github.com/introduction/flow/)

[Git flow](https://nvie.com/posts/a-successful-git-branching-model)


**Comments or Ideas:**
- TODO