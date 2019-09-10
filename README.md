# Encrypt your github repository
Sometimes you want to keep the history of some files on a public git repo, but don't want to let users see it.
This is where [git-crypt](https://github.com/AGWA/git-crypt) can help you, it allows to automatically decrypt/uncrypt specified files when you pull or push a repository.

## Installation
```
sudo apt-get install git-crypt
```

## Encrypt your github repository

1. Let's say you have a new repository and you want to encrypt `passwords.yaml`
```
README.md
encrypted/passwords.yaml
```

2. Create the git-crypt key and put here somewhere safe
```
git-crypt keygen gitcrypt-key
mv gitcrypt-key ~/.ssh
```

3. Go to your directory and add a `.gitattributes` to specify which files you want to encrypt, for example containing:
```
encrypted/passwords.yaml filter=git-crypt diff=git-crypt
```

4. Add, push and commit all the files **but not the one you want to encrypt**. This is verry important since if you commit everything you will have a commit showing your files that you want to encrypt.
```
git add README.md
git commit
git push
```

5. You can now initialize the git-crypt configruation
```
git-crypt init ~/.ssh/gitcrypt-key
```

6. Add the files taht you will encrypt
```
git add encrypted/passwords.yaml
```

7. Encrypt these files and check if they are indeed encrypted (it should output a long message beginning with ^@GITCRYPT^@)
```
git lock -f
```

8. If it is encrypted, you can now commit and push
```
git commit
git push
```

9. Later, to decrypt the files just do:
```
git-crypt unlock ~/.ssh/gitcrypt-key
```
