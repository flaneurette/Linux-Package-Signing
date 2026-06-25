# For update:

```
tar --exclude-vcs --exclude=debian -czf smash_1.3.orig.tar.gz smash-1.3
cd smash-1.3
debuild -S -sa -kD820A9F1F6945B042A63B50A2704A1EA4E14F1BB
cd ../
dput ppa:flaneurette/smash smash_1.3-0_source.changes
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
gpg --export --armor 2704A1EA4E14F1BB > public_key.asc
```

Decrypt Launchpad PGP message:

```
gpg --decrypt --output decrypted_file.txt encrypted_message.asc
```