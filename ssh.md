# ssh

- How to SSH into a VM easily?

Add all SSH config in `~/.ssh/config` or wherever your SSH config file, that you use, is stored. For example -

```
Host abcd-vm
  AddKeysToAgent yes
  UseKeychain yes
  User vm-username
  HostName host-name-or-ip
  IdentityFile ~/.ssh/your-ssh-private-key-to-access-vm
```

For the SSH to work the private key's corresponding public key has to be present in the VM's `authorized_keys` file, which is usually present in `~/.ssh/authorized_keys`. If it's not already present, you will have to append the file with your public key

And then you can easily use

```bash
$ ssh abcd-vm
```

The same config and idea can be used as part of `scp` commands too. For example, to copy a file into the VM's home directory

```bash
$ scp file.txt abcd-vm:~
```

- How to see verbose logs when SSHing into a VM?

You can use `-v`

```bash
$ ssh -v abcd-vm
```

This can be useful to debug what's going on in case of issues - failures, or when command running is stuck etc
