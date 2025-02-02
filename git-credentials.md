# git credentials

## macOS Keychain credentials

The [macOS Keychain credential helper](https://docs.github.com/en/get-started/getting-started-with-git/updating-credentials-from-the-macos-keychain) stores git creds in the macOS keychain. It allows `git` commands to authenticate to HTTPS URLs.

OSX installs the helper by default, eg:

```
git config --show-origin --get credential.helper
file:/Library/Developer/CommandLineTools/usr/share/git-core/gitconfig   osxkeychain
```

The creds are stored as keychain items named after the github host, eg: `github.com` or `github.acme.corp.com`.

To fetch keychain creds:

```
echo -e "host=github.com\nprotocol=https" | git credential-osxkeychain get
# or just
echo host=github.com | git credential-osxkeychain get
```

To delete (nb: paste each line in separately)

```
git credential-osxkeychain erase
host=github.com
protocol=https

```

This will remove the github.com item from the keychain.

Multiple users for the same host all use the same password, ie: the remote host `https://tekumara@github.com` will use the same password as `https://github.com`

## Git Credential Manager

The [Git Credential Manager](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git#git-credential-manager) is an credential helper for HTTPS urls. Similar to VS Code, it requires authorising an OAuth app and uses that to generate credentials for your github.com user.

On install, GCM will add itself as a credential helper:

```
[credential]
	helper =
	helper = /usr/local/share/gcm-core/git-credential-manager-core
[credential "https://dev.azure.com"]
	useHttpPath = true
```

credential.helper is multi-valued. The empty helper (`helper =`) line is [added to make GCM the exclusive helper](https://github.com/GitCredentialManager/git-credential-manager/issues/177#issuecomment-698250665).

To remove these git settings run `git-credential-manager-core unconfigure`.

GCM will first pop-up when pushing to an HTTPS url. You can sign in with your browser or a device login using a code. You will be asked to authorise the GCM app for your github account.

Once you have successfully pushed an oauth token will be stored in the login keychain named after the host, eg: `git:https://github.com`.

To revoke authorization for GCM, visit [Applications settings](https://github.com/settings/applications).

GCM supports [multiple users for the same host](https://github.com/GitCredentialManager/git-credential-manager/blob/main/docs/multiple-users.md).
