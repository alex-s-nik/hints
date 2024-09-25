**1. Undo a commit & redo**

**2. Добавить файл в последний коммит. Для этого используется опция --amend.**


**1. Undo a commit & redo**
```bash
$ git commit -m "Something terribly misguided" # (0: Your Accident)
$ git reset HEAD~                              # (1)
[ edit files as necessary ]                    # (2)
$ git add .                                    # (3)
$ git commit -c ORIG_HEAD                      # (4)
```
1. git reset is the command responsible for the undo. It will undo your last commit while leaving your working tree (the state of your files on disk) untouched. You'll need to add them again before you can commit them again.

2. Make corrections to working tree files.

3. git add anything that you want to include in your new commit.

4. Commit the changes, reusing the old commit message. reset copied the old head to .git/ORIG_HEAD; commit with -c ORIG_HEAD will open an editor, which initially contains the log message from the old commit and allows you to edit it.
If you do not need to edit the message, you could use the -C option.

[link](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)


Чтобы сохранить файл и выйти из редактора Vim, используйте команду :wq.

Для этого:

Нажмите Esc, чтобы переключиться в обычный режим.

Введите :wq.


**2. Добавить файл в последний коммит. Для этого используется опция --amend.**

Пример использования

Просмотрим историю коммитов.
```bash
$ git log

commit 5c4a8e76f951eb7ee157f4136257f6666fddf1d1
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:40:30 2016 +0300

    Changed 1.txt

commit 7f2ad8c26ad032800c049d0d6122c43410a5cbbc
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:39:30 2016 +0300

    Initial commit
```
Допустим существует файл который нужно добавить в предыдущий коммит.
```bash
$ git status

On branch master
Untracked files:
   (use "git add <file>..." to include in what will be committed)    
        test.txt
```
Добавьте этот файл в индекс при помощи команды git add.
```bash
$ git add --all

$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   test.txt
```
После этого вы можете добавить файл в последний коммит посредством использования --amend в команде git commit. Вы можете также изменить сообщение коммита добавив -m 'Commit message'. Чтобы оставить сообщение коммита тем же просто передайте пустую строку вместо сообщения -m ''.
```bash
$ git commit -m 'Added test' --amend

[master aad3e76] Added test
 Date: Sun Aug 28 14:40:30 2016 +0300
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 test.txt
```
Проверим историю коммитов.
```bash
$ git log --stat
commit aad3e7653cd76c4afa1a9272bd421493b4e3055c
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:40:30 2016 +0300

     Added test

 1.txt    | 3 ++-
 test.txt | 0
 2 files changed, 2 insertions(+), 1 deletion(-)

commit 7f2ad8c26ad032800c049d0d6122c43410a5cbbc
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:39:30 2016 +0300

     Initial commit

 1.txt | 1 +
 1 file changed, 1 insertion(+)
```
[link](https://ru.stackoverflow.com/questions/559711/%D0%9C%D0%BE%D0%B6%D0%BD%D0%BE-%D0%BB%D0%B8-%D0%B2-git-%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C-%D0%B5%D1%89%D0%B5-%D0%BE%D0%B4%D0%B8%D0%BD-%D1%84%D0%B0%D0%B9%D0%BB-%D0%B2-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BD%D0%B8%D0%B9-%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%BA%D0%BE%D0%BC%D0%B8%D1%82)
