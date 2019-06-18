# Encrypt your github repository
Sometimes you want to keep the history of some files on a public git repo, but don't want to let users see it.
This is where [git-crypt](https://github.com/AGWA/git-crypt) can help you, it allows to automatically decrypt/uncrypt specified files when you pull or push a repository.

## Installation
```
sudo apt-get install git-crypt
```

## Encrypt your github repository
1. Create the git-crypt key and put here somewhere safe
```
git-crypt keygen gitcrypt-key
mv gitcrypt-key ~/.ssh
```

2. Go to your directory where you have the repository

3. You can now initialize the git-crypt configruation
```
git-crypt init ~/.ssh/gitcrypt-key
```

4. Add a `.gitattributes` to specify which files you want to encrypt, for example containing:
```
encrypted/passwords.yaml filter=git-crypt diff=git-crypt
```

5. Add all the files, commit and push
```
git add .
git commit
git push
```
