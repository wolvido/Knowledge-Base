#### How does git really work? What's the point of it?
First, you have to know that there are many types of git development style.
In this note we will use Trunk-Based Development, this is a widespread style of git.
##### Trunk-Based Development
###### How it works?
In essence, it works by creating branches from the main, then once the branches are done, the branches are merged back into main.
The branches are small development features or bug fix.
>In Trunk-Based development, you do not push into main, you can only work on your branch and have it checked before merging.

**Multiple Devs can open many branches, so what if the merge conflicts?** This is where three way merging comes in.
##### Three way merging
For example:
- suppose you have the main branch: A → B → C
- You create a new branch (`feature-branch`) from commit C and add a new commit: D
So now, the branches look like this:
- `main`: A → B → C
- local `feature-branch`: A → B → C → D
While you're working on commit D, someone else adds a commit to `main`, creating a new commit `D2`:
- `main`: A → B → C → D2
Git will attempt to merge the changes between your branch and `main`, but since both your branch and `main` diverged from commit C, Git will have to figure out how to integrate your changes on: 
-  (D), 
- and (D2).
###### This is where **three-way merging** comes in. Git performs the merge as follows:
1. **Find the common ancestor** of both branches (in this case, commit C).
2. **Compare the changes** from commit C to D and the changes from commit C to D2.
3. Git then tries to apply both sets of changes (from D and D2) to the latest state of the branch.
###### Outcomes:
1. **No conflicts**: If D and D2 modify different files or different parts of the same file, Git will automatically merge the changes.
2. **Merge conflicts**: If both D and D2 modify the same lines of code or closely related parts of the code, Git won't know how to combine them automatically. It will pause the merge, mark the conflicting areas in the affected files, and ask you to manually resolve the conflicts.
After resolving any conflicts (if there are any), you commit the merge into main, and the history would look like this:
- `main`: A → B → C → D2 → M 
**M is the combined changes of D and D2 after resolving**
##### Keep in mind there are three types of merging:
###### **Normal Merge**
![[merge 1.png]]
Normal merge merges the feature into a new commit (F) and maintains the detailed commit history of the feature within (F). 
D and E is not included in the Main history, but it is accessible through F.
###### **Squash Merge**
![[squasj.png]]
Squash merge works like normal merge, but it omits the detailed history and just combines D and E into merge (F). 
D and E is omitted completely.
###### **Rebase Merge**
![[rebase.png]]
Rebase does not create a new (F) commit and instead it rebases all the feature commit directly to the main as if the history feature is part of main.
Like D and E is a direct push on main.
>[!info]
>Note that F is just a sample in this note, it is not a programming jargon.
###### So when to use what?
It depends greatly, if you just want a straight history go rebase, if you want full history go normal merge, if you want just want a summary of every feature then use squash.
##### Inverse Merge 
You can also merge the main into your feature in a sort of inverse merge direction.
Your main looks like this:
`A → B → C → D2` 
	It was updated from C to D2, while you were working on D.
If you merge main into feature, it would look like this:
`A → B → C → D → D2`
D2 would come last since by its commit history, you were working on D first and added D2 later on.
**This is useful if you want to resolve the three way conflict on your feature, rather than on a main merge request/pull request**.
So once you decide to merge the feature to main, there will be no conflict and it will result in:
`A → B → C → D2 → M` 
M is your feature with D2 baked in.
#### Notes:
- NEVER commit whole, always commit one by one per feature/fix.
- Remember to sync local to main after merging.
- Don't confuse pull request from pull. 
	- Pull request (PR) is more like merge request where you request for a feature to be merged.
	- Git pull is pulling code from GitHub.