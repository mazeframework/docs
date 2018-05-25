# Encrypt

The `encrypt` command allows you to encrypt and edit your environment settings. This allows you to store production secrets in your repo safely.

Here is a list of the commands available:

```text
maze encrypt [OPTIONS] [ENV]

Arguments:
  ENV  Environment settings to encrypt (default: production)

Options:
  -e, --editor  Prefered Editor: [vim, nano, pico, etc]
                (default: vim)
  --noedit      Skip editing and just encrypt
```

## Editing Encrypted Files

The command`maze encrypt production` will use the secret key in .`encryption_key` or `ENV[MAZE_ENCRYPTION_KEY]` to decrypt `config/environments/.production.enc` and open it in your favorite editor.

When you save and exit it will encrypt again.

![Maze Encrypt Demo](https://raw.githubusercontent.com/mazeframework/site-assets/master/videos/maze_encrypt.gif)

## Encrypt unencrypted environment settings

`maze encrypt development` will encrypt `config/environments/development.yml` using same keys as above.

Editor will be opened if file is already encrypted.

`maze encrypt development --noedit` will encrypt file if unencrypted but do nothing if it's already encrypted. Editor will not be opened.

{% hint style="info" %}
Production is encrypted by default.
{% endhint %}

## Note about Maze Encryption Key

Keep track of the values of `.encryption_key` or `ENV[MAZE_ENCRYPTION_KEY]`. If you lose these you will not be able to decrypt an encrypted file.

When a new project is created the file `.encryption_key` is created with a random key. This is added to `gitignore` by default as it should never be added to your repo.

If you need to encrypt or decrypt on another development box or server you will need to manually move `.encryption_key` or set the value of `ENV[MAZE_ENCRYPTION_KEY]` on that computer.

If your server can't read your encrypted settings it will use the default ones.

