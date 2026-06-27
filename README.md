Simple steps for packgae creation, signing and uploading to ppa.launchpad.net.

# For update:

```
tar --exclude-vcs --exclude=debian -czf smash_1.3.orig.tar.gz smash-1.3
cd smash-1.3
debuild -S -sa -kEE274F961CF4A8143BC68EEFB240191A0B2B7B8C
cd ../
dput ppa:flaneurette/smash smash_1.3-0_source.changes

or:

dput -c ~/.dput.cf  smash_1.3-0_source.changes
```

nano ~/.dput.cf

```
nano ~/.dput.cf

[DEFAULT]
# Default settings (applies to all uploads)
fqdn = upload.debian.org
method = ftp
incoming = ftp-master
login = anonymous

[ppa.launchpad.net]
fqdn = ppa.launchpad.net
method = sftp
incoming = ~flaneurette/ubuntu/smash
login = flaneurette
ssh_config_options = StrictHostKeyChecking=no

[ftp-master]
fqdn = ppa.launchpad.net
method = sftp
incoming = ~flaneurette/ubuntu/smash
login = flaneurette
```

Generate a new GPG key:

```
gpg --full-generate-key
```

List your keys to find the new key ID:

```
gpg --list-secret-keys --keyid-format LONG
```

Export the new public key:

```
gpg --export --armor B240191A0B2B7B8C > public_key.asc
```

Decrypt Launchpad PGP message:

```
gpg --decrypt --output decrypted_file.txt encrypted_message.asc
```
