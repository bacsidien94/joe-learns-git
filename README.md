# joe-learns-git

```
Joe learns git 🐱‍💻📚
but at first let's learn how to use git to collaborate with others
thus, I share some basic commands as a get-started-kit.
Here we go...
```
## Basic Git Command

### Status - Init - Pull - Clone Checkout

```
Check homebrew status first
brew update
Git installation using homebrew
brew install git 
Check git version
$ git --version
before doing anything, need to navigate to the location of the local repository for example
cd /Users/tiengiap/Dropbox/Repository/joe-geek 
Linux syntax for the terminal can be used, for example, list all files in the current directory
ls 
Add your Github email and username to git
$ git config --global user.email "yourGitHub@email.com"
$ git config --global user.name "your GitHub username"
to create a local repository
git init  
Indicate remote repos which connect to this local repos
git remote add origin “remote repository path”
to pull from remote repos to local repos
$ git pull origin master 
clone
$ git clone repo_name //để clone một trong những repo của bạn
$ git clone username/repo_name //để clone của người khác
to check if there is any modification
$ git status 
```
### Add - Commit - Push

```
Add modified file from local repos to staging;  after adding, the status will be “Unstage”
$ git add ‘filename’ 
$ git add -A //stages all changes; is equivalent to git add --all
$ git add .  //stages new files and modifications, without deletions
$ git add -u //stages modifications and deletions, without new files; is equivalent to git add --update
$ git add * //adds modified and any new files 
 to commit a new file to Staging; after commitment, the status will be “Staged”
$ git commit -m “put change log description”  
 push staged file from staging to the remote repository
$ git push -u origin master
Push branch từ Local lên Remote với tên khác:
Bình thường, việc push một branch ở local lên remote branch được thực hiện bằng cách: 
$ git push <remote_name> <branch_name>
Tuy nhiên việc push dưới một tên khác sẽ có khác biệt, cụ thể: 
$ git push <remote_name> <local_branch_name>:<remote_branch_name>
```

### Checkout - Merge

```
Kiểm tra danh sách branch: 
$ git branch //để thực thi trên remote repo, ta chỉ cần cho thêm tùy chọn -r hoặc --remote
to switch between branch
$ git checkout <branch name> 
Xóa branch:
khi đang ở branch khác: $ git branch -d <branch_name>
khi đang ở branch cùng tên với remote branch muốn xóa: $ git push <remote_name> -d <branch_name>
Rebase và merge:
Rebase:
 $ git checkout <branch_name>
 $ git rebase <rebase_branch_name>
Cách thực hiện: Lấy code từ rebase_branch_name sau đó từ những commit ở đó tạo ra những commit tương tự lên branch_name. Thực hiện rebase thì các commit đã tồn tại bị bỏ đi và tái tạo lại các commit tương tự nhưng thực ra là khác biệt. Điều này làm lịch sử commit ở local và remote khác nhau.
Đặc điểm: các commit của nhánh được tạo mới sẽ nằm liền mạch, và các commit của rebase-branch sẽ là các commit mới nhất.
Merge:
$ git checkout <branch_name>
 $ git merge <branch_2_name>

Cách thực hiện: git dùng 2 bản commit cuối cùng của từng nhánh rồi tích hợp lại với nhau tạo thành 1 commit mới theo kiểu hình thoi. Thực hiện merge thì các commit đã tồn tại không bị thay đổi, chỉ tạo ra 1 commit mới tích hợp của 2 commit mới nhất.
Đặc điểm: các commit của 2 nhánh được sắp xếp theo thời gian tạo commit.
Gộp commit:
Tùy vào từng môi trường, công ty khác nhau sẽ có những yêu cầu khác nhau về việc quản lý commit. Ví dụ công ty yêu cầu mỗi request bạn gửi lên chỉ có duy nhất 1 commit. Bạn vào kiểm tra thì lại thấy nhiều hơn, thì công việc của bạn là gộp những commit ấy lại. Và việc thực hiện sẽ ra sao?
$ git rebase -i <id_commit_end> || $ git rebase -i HEAD~<index>
<id_commit_end> là id của commit cuối trong nhóm cần gộp.
<index>: số commit cần gộp. Sau đó, cửa sổ làm việc hiện lên, Ta có các lựa chọn pick|squash|fixup các commit trước khi save.
Sau đó kiểm tra lại bằng lệnh: $ git log --oneline xem commit đã được gộp thành công hay chưa.
 ```
 
### Git stash

```
Khi đang làm việc với một branch rồi bạn chợt nhận ra mình cần sửa ở branch cũ, bạn sẽ cần checkout và phải commit những thay đổi. Tuy nhiên, bạn chỉ cần lưu nó lại mà chưa commit, và git stash sẽ giúp bạn. Ngoài ra, có 1 số tuỳ chọn như:
Xem lại lịch sử thay đổi: $ git stash list
Xem lại lịch sử thay đổi cùng nội dung của nó: $ git stash list -p
Xem lại lịch sử thay đổi: $ git stash list
Xem lại lịch sử thay đổi cụ thể của lần 1: $ git stash show stash@{1}
Apply thay đổi của lần 1: $ git stash apply stash@{1}
Xoá thay đổi: $ git stash drop stash@{1}
Xoá toàn bộ: $ git stash clear
```

### Reset

```
Trong cuộc sống, mọi hành động thì không thể "hoàn tác" được. Nhưng khi làm việc với máy tính, Ctrl-Z luôn sẵn sàng để sửa chữa sai lầm cho bạn, và git cung cấp cho bạn 3 phương pháp:
$ git reset <commit_id> // khi ta muốn di chuyển HEAD đến commit reset và giữ nguyên tất cả thay đổi của file đến vị trị hiện tại. Tuy nhiên sẽ loại bỏ thay đổi khỏi stage.
$ git reset --hard <commit_id> khi nó vẫn di chuyển HEAD đến commit reset nhưng sẽ loại bỏ tất cả thay đổi của file sau commit reset.
$ git reset --soft <commit_id> khi muốn di chuyển HEAD đến commit reset và có ưu điểm là sẽ giữ nguyên tất cả thay đổi của file và các thay đổi ở stage. 
Vì vậy reset --soft được khuyến khích sử dụng hơn, tuy vậy, bạn cũng nên tùy chọn phù hợp với hoàn cảnh và mục đích bạn mong muốn.
```

### Reference

```
tham khảo các bài viết từ Viblo https://viblo.asia/search?q=git 
```
