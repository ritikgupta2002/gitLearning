    Why do we need VCS?
            
Revert back to previous states.
Compare changes with previous states to find bugs 
Useful for working in teams, tracks all changes made by each team member 
So that it becomes easy to find the bug if present 
If data loss from your local machine , then whole code will be lost so 
In that phase we need git which stores our code in the remote server so that if there is a data loss in your machine we can easily download it 

    What is the working directory ?

The contents of your project folder (the folders and files you find within it) are represented by the working directory.Every directory has its own repository .

    What is the repository ?

.git folder (which is a hidden folder ) represents the repository .
In this folder we store the tracking record of each file in the working directory 

Within the .git folder there are two "places" that should be mentioned, the staging area (represented by the index file) and the commit history (represented by the objects folder).

The staging area is sort of like a rough draft space. Whenever you are done working on a file (or files) in your working directory and you want to update the changes, you have to copy them to the staging area (using the git add command).

Once you have all the files that you want to update in the next version of your project in the staging area, you are ready to save them in the next version of your project which is called a commit. You do this using the git commit command.

A commit is basically a version of your project and each commit has a 40 character hash (40 letters and numbers) and this hash acts like a name for the commit, it's a way to refer to it.

The commits are in the commit history (objects folder).
            
So in order to add a file to our repository:-

First we create a file in our project folder so it goes in our working directory
Then we add it to the staging area (using the git add command)
And then it becomes part of a commit in our commit history (using the git commit command.
                                  Or (last point )
Then you can use 'git commit' to further push your changes from staging area to local repo(which is a copy of your master repo)
 
                      Types of VCS
 
Centralised VCS :- 

1.In centralised source control, there is a server and a client. The server is the master repository that contains all of the versions of the code.

2.The basic workflow involved in the centralised source control is getting the latest version of the code(not all versions ) from a central repository that will contain other people’s code(latest version modifications) as well, then make your own changes in the code, and then committing or merging those changes into the central repository straight forward .
 #Thus making a new version of the source code, So everything is centralised in this   model. 
 #There will be just one repository and that will contain all the history or version of the code and different branches of the code.i.e master repo

3.The need for the internet is important .

#
 Distributed VCS :- 

git is a distributed vcs 

1.In distributed version control most of the mechanism or model applies the same as centralised. The only major difference you will find here is, instead of one single repository which is the server or master repository , here every single developer or client has their own server or local repo ,and they will have a copy of the entire history or version of the code and all of its branches in their local server or machine( local repo is kind of a mirror image of master repo )

2.Basically, every client or user can work locally and disconnected which is more convenient than centralised source control and that’s why it is called distributed. 

3.So when you start working on a project, you clone the code from the master repository in your own hard drive, then you get the code from your own repository to make changes and after doing changes, you commit your changes to your local repository and at this point, your local repository will have ‘change sets‘ but it is still disconnected with the master repository (master repository will have different ‘sets of changes‘ from each and every individual developer’s repository), so to communicate with it, you issue a request to the master repository and push your local repository code to the master repository. 

Getting the new change from a repository is called “pulling” and merging your local repository’s ‘set of changes’ is called “pushing“. 
It doesn’t follow the way of communicating or merging the code straight forward to the master repository after making changes
Firstly you commit all the changes in your own server or local repository and then the set of changes’ will merge to the master repository. 

4.DVCS is faster than CVCS because you don’t need to communicate with the remote server for each and every command. You do everything locally which gives you the benefit to work faster than CVCS.

5.If the project has a long history or the project contain large binary files, in that case, downloading the entire project in DVCS can take more time and space than usual, whereas in CVCS you just need to get few lines of code because you don’t need to save the entire history or complete project in your own server so there is no requirement for additional space.

6.If the main server goes down or it crashes in DVCS, you can still get the backup or entire history of the code from your local repository or server where all  the version of the code is already saved. This is not in the case of CVCS, there is just a single remote server that has the entire code history.

7.files remain in 3 states in git shown in the image below .

    untrack
    Staged,
    committed


     

 
       
  
  




This above image is the life cycle of the git file .


Some basic commands 

to check the version 

     1)git --version 

to initiate a new repository 

     1)  git init <filename>
this will create a .git folder in the current directory and remove the previous local repo in the current dir.

to check what are the files in our directory 

     1)  ls 

to give the alias to a command 

    1)git config --global alias.cmt ‘commit’ [this is for global use you can do it for local by writing local inplace of global ]
we can use git cmt instead of git commit in future.

to get help 

    1) git help

to check the status 

    1) git status 

to see what are the files which are being tracked by git 

    1)git ls-files(this contains all the files which are being committed and are on staging area )

to stage the file 

     1)git add . (to add all the files in the directory in the staging area )

     2)git add <filename1> <filename2> ....etc (used to add selected file to staging area)

to commit the file 

     1) git commit -m "message"

To amend the commit 

     1)git commit --amend 

It is not a good practice to do dirty commits like for ex we wrote some code and did the commit after doing commit we realised that we have forgotten to include some 5-6 line code ,now what do we do? , if we add  code to the file  and then again do the next commit that would not be a good practice that would be a dirty commit ,because every commit has a very imp significance , so what you do is you do correction in  the previous commit only by using this command 

So how to perform this command :-  this is not so straightforward :0
As you have realised that you have to make some changes to the file already committed 
           now do changes to the file that you have to make 
 after that follow the steps :-
Do git add .
After that write git commit --amend 
A new screen will open so now first press ‘i’ to insert and make changes in the last commit message after that press esc 
 then write :wq 

in this image i forgot to write “you “ at the end but the file already committed with message -” messages “

Now make changes to the file demo.txt and do git add . 

Then do git commit --amend 

Now press i and change the commit message with “messages final”and then press escape then write :wq and then you can see the git log the new commit replaced the previous commit (which was showing messages)



How to specifically amend any commit?


git rebase --interactive HEAD~4 (if you want to basically amend the fourth commit ) 
Or 
git rebase --interactive <commit id >^ (if the commit is basically too down and you can't count)

Then write edit instead of pick in front of the particular commit 
After that exit then you will be taken to the previous stage when you did that commit so now make changes after that stage all your changes then write 

git commit --all --amend --no-edit  
Or 
git commit -amend -m “some message you want to write “

After  that if there are conflicts solve them manually then 
Write  git rebase --continue to move to the stage where you left .
If you can’t resolve the conflicts then write 
git rebase --abort ->  this command Git will return you to your branch's state as it was before git rebase was called.

NOTE:- make sure you have not pushed ,if you have pushed then you can't change otherwise you can .

NOTE:-Lekin ye command jab hi kam karega jab tak humne code ko push nhi kiya ,code hamari local repo me hai 
Agar last commit tak sb push ho chuka hai then hum koi bhi commit ko amend nhi kr skte.


so to  untrack the files 

0)git rm <filename> it will remove the file ,after that do a commit after running this command (you use this command when you know the file is committed )working directory se bhi removed and staging area se bhi remove hogi file .

1)git rm -f <filename> this is used when you want to delete the modified file which may not be in staging area(but the file has to be once staged in its lifetime) ,if you use the first command to delete the modified file then there will be an error saying this is modified file if you remove this you can't retrieve if you want to delete write -f so if you use this command (-f wala) then modified file working directory se bhi removed and staging area se bhi remove hogi file agar stage kr rkha hai modifications krne ke baad me .

2)git rm --cached<filename> this is used when you want to untrack the file but don't want to delete the file from the working directory (whether file is committed or on staged area doesn't matter it will go to untracking state after doing this command ) 

to rename a file or move a file 

1) git mv filename1 renamedfilename1
 [it is good because if the files have already been staged , by using this command the renamed file will also be directly in staged area only 


to add projects on github use these commands

1)git remote add origin https://github.com/guptaritik2002/repositoryname

When you clone someones repo and make changes and when you push it to your newly created repo on github it will show 403 error as you don't have rights to make changes to the origin (here origin at present is owners repo )which is not your repo it is by default the repo of the owner of the code jahan se clone kiya hai so you have to change this variable name origin to something diff may be myorigin and after that push it .

2)git branch -M main
3)git push -u origin main 

From the next time you can just write git push  to push changes from the local repo to github 
Always press q to end the ongoing process .

To get the additional code that is added after commit 

1) git diff <filename> 
As you can see in the below image, there is a “+” symbol, which means that a new line is added,if there is a “-” symbol, then a line is deleted.

user@radhakrishnadas MINGW64 ~/myproject (main
$ git diff bye.txt
diff --git a/bye.txt b/bye.txt
index 8a50447..b03e481 100644
diff --git a/bye.txt b/bye.txt
--- a/bye.txt
+++ b/bye.txt
@@ -1,2 +1,2 @@
 hello shri krishna and radha rani i love you
 hello shri krishna and radha rani i love you
-dfdfdfdfdf
\ No newline at end of file
+sddsds
\ No newline at end of file


How To Clone a repo? 

1) git clone <url>  
With git clone you clone the repo with its .git folder .
2) git clone <url> folder name (all project files will be copied to this folder this folder will be inside the parent folder  )



Get changes made to a file line by line with author who made the change and the date of modification
1)git blame <filename>

$ git blame hello.txt
9f4a5c50 (guptaritik2002 2022-03-20 10:01:09 +0530
1) hii everyone welcome to hello git
608c40c1 (guptaritik2002 2022-03-20 10:34:37 +0530
2) i everyone this is just for demo
ff1fb59e (guptaritik2002 2022-03-20 10:39:46 +0530
3) hii
ff1fb59e (guptaritik2002 2022-03-20 10:39:46 +0530
4) hello
ff1fb59e (guptaritik2002 2022-03-20 10:39:46 +0530
5) everyone



How to view the commits made 
1) git log 
Press enter to view the commits and when you are done seeing the commits press q to end 
2)git log -2 ( used to view the last 2 commits)

What is the git branch ? learn branching by doing click me  

1)git branch < branch name  > to create a new branch
2)git branch (to see the list of all branches)
3)git branch -d <branch_name>( to delete the branch)
4)git branch -m <old_branch_name> <new_branch_name>(to rename branch)
1. git branch is an option, wherein you create a separate branch from the master branch,this branch has all the code which the main branch have,so this branch can be used for testing and debugging purposes.
2. You might be developing a feature and that you don’t want to continue in the master branch because it is live, so use the newly created branch till the testing has been completed.
3. In that case, you will create a separate branch and work in that branch, once the branch is stable, then you can proceed to merge with the master branch.
We shall see the list of options that “git branch” is having through series of examples:
1. To create a new branch, use “git branch <branch_name>”, then we check the list of branches by using the “git branch” command.

2. To delete a branch, use “git branch -d <branch_name>”
3. To rename a branch, use “git branch -m <old_branch_name> <new_branch_name>”
 
What is head in Git ?
HEAD is like a pointer that points to the current branch. When you checkout a different branch, HEAD changes to point to the new one. The current HEAD is local to each repository, and is therefore individual for each developer.
 
git checkout command 
 how to use the new branch ?
1. To use the new branch use git checkout<branch name >
One you have switched to a new branch, you can start making your changes.
2. To switch to main branch, use git checkout -m main 
3. To create and switch to a branch, use git checkout -b <branch_name> 
#Another use of the checkout command is to go back to the last committed state from the modified state .for ex there are files like b.txt,a.txt,c.txt ….etc  if their are all committed now and then we thought of making some changes in all the files , so all files now have modified state , so after doing changes we realised that c.txt and b.txt should not be modified now maybe we can do at later stages but modification are already done so what we do is we use this command to go back to previous committed state for these files b.txt and c.txt .
                                                        Or in simple words 
     (modified state ->most recently committed state or recent staged state )
 
How to use this :- git checkout --(space)<filename1> <filename2> ……….etc
                                                            Or
similar command with  git restore <filename1> <filename2> ….etc same work as above checkout wala command 
NOTE:- recently committed to samajh me aata hai ye recently staged kya hai ?
Very imp:-Forex koi file me pehle modification hue fir maine usko commit kiya fir dobara kucch modifications kiya fir unko stage bhi kr liya ,fir se kuch modification kiya  fir mujhe laga ye jo ye recent modifications hai ye galat hai so i have to revert back to most recent staged or committed state ,then now if i use use above commands then it will go back to most recent staged or committed state here the most recent is the staged state so we go their .
NOTE:-Remember filename dalte smay command me ek space chahiye hota hai after hyphens, between multiple filenames 
NOTE:- Above commands will only work for the files which were at least once committed or staged  in the past and now modified so after using these above commands the files will then reach to the most recently committed state or staged state ,otherwise the commands will not work.
#In the above commands the changes we made were lost as we run that command. What if we save changes in the local repo somewhere so that when we need them we can use them so we do not have to do extra labour.so their comes the next command git stash 
Git stash  (modified state ->recent committed state with storing modifications)
#Simply write git stash and all the modified files will now go back to their last committed state and all the changes made in the respective files will be saved in stack ( good for understanding ) in local repo so whenever we need them we can get them easily by doing git stash pop in all the files whose changes are saved using git stash 
To stash a particular file only :- git stash --(space)<filename1><filename2>..etc.
To stash pop a particular file :- first use git stash list
Then see the stash name it would be something like stash@{0} remember it Then write this command :-
git restore -s stash@{0} --(space)<filename1`><filename2>
                  
#git  stash clear :- this command is used to clear the saved modifications in local repo in stack form .
NOTE:- if the file is not even once committed and staged then you cant use stash command but if the file is at least once staged then you can use this command , but the difference is that when your file is not even once committed but only staged and even after staging let say you do some modifications now the status is modified and then run this command the whole file will be deleted and when you git stash pop  the whole file will be retrieved and everything is retained even the modifications we did at the end ,but this time the status of the file is staged ,but if the file is even once committed no matter how much times staging done after that if you use this command you will go back to that most recent committed state and safe the modifications done after that .
 
git merge command 
Once you have checked-out to a new branch and made the changes, how do you merge those changes to a new branch?
To do that, use the “git merge” option.
Before we merge, we shall add the below line to myProg.c file in the new branch.
printf(“New line added from new_feature branch”);
Once the changes have been completed, you need to add the changes by using “git add .” and commit the changes by using “git commit -m “new feature'' command.
This will commit the changes to the “new_feature” branch.
Now that we have made the changes and committed the changes to the new branch, how to merge them to the master branch?
To do that, it is a 2 step process:
Step 1: Checkout to master branch by using git checkout -m main
Step 2: Use git merge <branch_name> to merge that branch to the master branch
Example:
I have merged the “new_feature” branch to the “master” branch.

Merge happen with 2 strategies :-
1)recursive strategy {ek naya commit banta hai for merging the branches}
2) fastforwarding strategy{no new commit formed only shifting of pointer happens }
NOTE:-we should delete the branches once they are merged with the main branch 
NOTE:- use git log --all --decorate --oneline --graph to see git log in graph ,see all merges in graph form 
NOTE:- branches hamesha latest commit ko point karte hai .
Merge conflicts 
When two developers in a team work in their respective branches then if both dev do  some changes on the same file and on  some similar code lines then there will be a conflict when both developers will finally merge their branch with the main branch .

                            This is how it looks (this is the merge conflict )
 
How to use the .gitignore file ?

Make the .gitignore file in your repository and then add the files in it which you don't want git to track  

Some shortcuts 
*.a ( * means all  ) if you write this in your .gitignore file git will ignore all files which have .a as extension 
*.[oa] ( means all the files which have either .o extension or .a extension should be ignored )
!lib.a( for example after sometime we find that that out of all .a files we ignored one file lib.a which  should not be ignored so we write:-  not of lib.a which means do not ignore lib.a  )
todo( this will ignore all the todo files in the repo {here todo is just an example for explanation} but if you want to ignore only the todo files of current working directory then write like this /todo )
l?b.?xt (? matches with single character ,for ex if there are files like 
lib.txt, lob.txt, ldb.pxt then as we can see in place of first  question mark i,o,d can come and in place of second question mark t,p can come so all files with this common syntax written in blue will be ignored )
To ignore all the files of the dir write like this /dirname 

NOTE:-          Whenever you are adding a file in .gitignore file then follow these steps 
If the file is not once committed, doesn't matter you have changed it or not 
Then directly add the file name to .gitignore file 
 If the file is committed even once then directly adding it to the .gitignore will not work you have to first of all 
commit the changes made then 
Add the name of the file in the .gitignore file
 then on the git bash write git rm --cached filename 
, then git add . 
 then git commit -m “ message”
After that everything will work fine
      
   How to comment in .gitignore is very simply use  # before filename 
  Forex = #hello.txt this file is commented means this file now  getting tracked

NOTE:-   like if you commit like for example after modifying 7 files (just an example) then you push them on you remote server (github) you will see that all those 7 files show the same commit message (this seems pretty logical also ) this happens so that one when come back in the history can know with this commit these files were modified , in professional world every commit has a value /importance with certain commit you do certain tasks , 2 commits for same task is not recommended already discussed about the dirty commits.

Git reset command (staging area -> modified state )
                                  (staging area -> untracked state only for empty files)


git reset HEAD <filename>(use to unstage the files)
Demerit of this command :-This variation of git reset command will have no effect if you use this command for a committed file .
#This command is important because for forex you have two files on the staging area and then you realise oh shit ! These files are of diff tasks we should have diff commit for both  so what to do now , there comes this command we use this so that we can go back from staging area to modified stage . So let say file a.txt and b,txt both are in the staging area ,but now we decided to commit separately for  b.txt so we use this command because of which b.txt goes back to the modified stage , after that you can commit separately for both .
NOTE:- similar command 
git restore --staged <filename> <filename2>.....etc (use to unstage the files)
In this command also if you have staged a particular file you can unstage it so that you can come back to the modified stage .

NOTE:- if both the commands git reset HEAD <filename> or git restore --staged <filename> are used for a  file (EMPTY FILE) which is untracked previous to the state now which is staged then after using these commands on these empty files you will again reach to untracked state 

Variations of git reset command 

git reset --soft  HEAD~2 (this will point head to 2 commits before from now on but whatever the changes made in first 2 commits will be still kept but the files will be in staging area )

git reset --mixed HEAD~2 (this will point head to 2 commits before from now on but whatever the changes made in first 2 commits will be still kept but the files will be in untacked area or in  unstaged area )

This command can be used to untrack or unstage only the committed files .
while git reset HEAD<filename> is used to unstage the files which are in the staging area only it cant unstage the committed files .

git reset --hard HEAD~2 ( this will point head to 2 commits before from now on And the starting 2 commits will be totally discarded all changes done in those 2 commits will be lost )

 staging area ko index area bhi bolte hain .
 HEAD always points to the latest commit in the branch .
Working dir likha hai jahan par vahan pr hum untracked state                       soch skte hai 

git fetch
* “git fetch” command is used to pull the latest changes from the remote repository to your local repository.
* It will not merge with your changes. Hence your working repository will remain safe from merge conflicts.
* You will use “git fetch” to know the snapshot of what others are working on.
Example:
To fetch a remote repository use:
“git fetch <remote_repository_url>” or git fetch origin 
(origin me remote repo ka link hota hai )
After doing git fetch do git merge so to see changes in working directory in your local repo then you can do git push 
NOTE:- when you clone a remote repo 2 branches are formed one is your local branch and other is remote branch .
As i said both branch has to point to latest commits and the work of the remote branch is that to point to a commit where remote repo main branch is pointing but let say their are some changes in remote repo and because our remote branch and  remote repo are not in 24*7 sync so may be remote repo will point to some other commit which remote branch does not point to .so when we basically git push the error will come so we have to fetch the latest commits from the remote repo 
git  fetch  origin then do get merge then do git add and git commit uske baad git push 
NOTE:- git pull = git fetch command +git merge 
How to use git pull ? ans -> git pull origin or git pull < remote repo link >
NOTE:- A VERY IMP ANALYSIS
When we do a clone of anyone’s repo we do git clone <repo url> After  that all the folders of his repo will come to our working dir , after that  if you made some changes and do git push you will get error because you don't have rights to push in the owner's project repo ,this happens because the when you clone the remote repo ,currently the remote repo link is set to owners repo ,you can see it by doing git remote -v ,you will get the link of owners repo now what to do now ? Obviously if you want to push changes ,but without permission you can't push ,either you take permission or make your own remote repo online in github and whatever changes you make in your project and when you push it should happen in your remote repo so how to do that ? very easy what we have to do is to add our remote repo link in our working dir by using                                                                            git remote add myrepo_name <repo link>,after that write                              git branch -M main m after that write git push myrepo_name main now your working dir has all the folders of the project you want to work , your working dir has remote repo link set to your remote repo of your github now whatever you push will reflect in your remote repo simple :) 
NOTE :- If you are cloning your repo so after cloning no need to setup the remote link just make changes then  stage , commit and  write git push 
NOTE:-To remove a remote repo use git remote rm <myrepo_Name>           repo_Name should be the name that you used to save the repo url.          
For ex :- git remote add myrepo_name<repo link> 
then we can do  git remote rm < myrepo_name>
Forex To fetch a repo use git fetch <myrepo_name>       
So whenever adding remote repo do these steps ( in our system we have cloned from the owners repo so we have to setup the remote link to our newly created repo ):-
git remote add myrepo_name< remote repo link>
git branch -M main
git push <myrepo_name> main
When your local repo is not in sync with remote server or git repo (these steps are done when remote repo is not newly created means the repo has some files that your local repo does not have,so first we have to sync both)

git remote add myrepo_name< remote repo link>
git branch -M main
git pull --rebase myrepo_name main 
git push <myrepo_name> main
Note :- You do only this first time after that you push changes by writing 
git push 
git push 
“git push” command is used to push the local changes to a remote repository.
Syntax: git push <myrepo_name> main
git rebase 
The primary reason for rebasing is to maintain a linear project history. 
Here we can see we have a branch named ‘feature’  we have lot of commits in this branch also and in main branch also now if we want to merge this feature to main branch we could have used git merge feature but it would look like this which is non linear merging 
 But if git rebase is used then it would like this 
        
 
                                           
 
 
 
 
 



Here we can see the linear history of commits that have been created .
You have two options for integrating your feature into the main branch: 
merging directly or rebasing and then merging. The former option results in a 3-way merge and a merge commit, while the latter results in a fast-forward merge and a perfectly linear history.

              Image after merging(fast forward merging)
rebasing is like saying, “I want to base my changes on what everybody has already done.”Rebase actually rewrite your commit history “ 

git rebase is always used in the feature branch not on the main branch like this 
git rebase feature

When not to do git rebase ?
Use git rebase only when you are doing development alone ,which means no one is coming to your repo and cloning and making changes in your repo otherwise don't use it .

Kabhi koi kaam push kr rkha hai to fir rebase kabhi nhi krna .


How to contribute to any project ?
Clone 
Fork 
Set the remote link to your forked repo ,pehle bata rakha hai 2 step process 
Push  the changes 
And then click on contribute ,click on pull request 
Create pull request 
Title dalo
And then tell about what you improved in detail 


git revert

For linear commits :-
       git revert <commit id>
       git revert <revert commit id>

This command is used to revert the changes done but it does not rewrite history like git reset --hard (this deletes all the changes and undo the commit ) while this git revert undo the commit and changes but it does not deletes the changes ,what happens actually is that a new commit will be prepared who will have all the commit changes except the the commit that you want to delete or undo so now head will point to this new commit(known as revert commit ) . while the previous commit which you want to undo is still not deleted it is there but head does not point over their head points to the new commit created(known as revert commit ) who has all changes of the all commits (from the last push)except the commit who you want to delete ,one thing more i want to tell is that we can literally revert any commit in between not just the first one , just write git revert <commit id> well if we talk about how to get it back than we will have to write git revert <revert commit id>
In that case we will get back the commit that we have undo ,but this all i have told is good when linear commits have been done (commits done on one branch only)
Here c2* is created as the revert commit; it has all changes of the commits (c0,c1,c3,c4) except c2 which we want to undo; we can see the commit which we want to undo has not been deleted .



















Here we can see a new commit is created c2’’ { when we revert the revert commit c2’ (this is done to get c2 back )  this new commit c2’’ has all the commit changes c0 to c4}

For nonlinear commits (means branches are their ):-


Undo the merge :- git reset --hard HEAD~1

If you already have repository on remote server that have already some fies












