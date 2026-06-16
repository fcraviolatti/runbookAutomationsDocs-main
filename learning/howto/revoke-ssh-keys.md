---
title: "Revoke SSH Keys"
source_url: https://docs.rundeck.com/docs/learning/howto/revoke-ssh-keys.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Revoke SSH Keys

This document assumes that your OpenSSH installationâ€™s configuration files reside in `/etc/ssh`. If they do not then please adjust accordingly. All commands were ran/tested on a fresh installation of [Ubuntu 21:10 Impish](https://releases.ubuntu.com/21.10/).

## What is Key Revocation?

OpenSSH in versions past 5.4/5.4p1 (released in 2010) support the ability to revoke keys. Once a key is added to the revocation list it cannot be used for user or host authentication and will trigger a warning if it used.

Firstly, a revocation file must exist or *sshd* disables key based authentication, so as a precautionary step make sure the `ssh_revoked_keys` file exists.

<div class="language-text line-numbers-mode">

``` text
rundeck@f00:/# touch /etc/ssh/sshd_revoked_keys
rundeck@f00:/# ls -l /etc/ssh/sshd_revoked_keys
-rw-r--r-- 1 root root 0 Apr 13 10:27 /etc/ssh/sshd_revoked_keys
```

</div>

Once this file exists, you can modify your *sshd_config* to add the â€œRevokedKeysâ€? section.

If you have the newer style /etc/ssh/sshd_config.d/ configuration you can run. (root privileges may be required)

<div class="language-text line-numbers-mode">

``` text
echo "RevokedKeys /etc/ssh/sshd_revoked_keys" >/etc/ssh/sshd_config.d/revokekeys.conf
```

</div>

If you are using a single sshd_config file only. (root privileges may be required)

<div class="language-text line-numbers-mode">

``` text
( echo ; echo "RevokedKeys /etc/ssh/sshd_revoked_keys" ) >>/etc/ssh/sshd_config
```

</div>

Then reload the sshd config by whatever means the OS desires (systemd, upstart, sysvinit, /etc/init.d/ssh reload,` kill -s HUP "$(cat /var/run/sshd.pid 2>/dev/null || pidof 'sshd' 2>/dev/null)`").

If you reload without that file, you will see the following in your sshdâ€™s logs when trying to use key based authentication, and will not be able to log in with them! (debug1 and debug2 are addition levels to the default as way of illustration.)

The Error checking authentication key line is output as a regular log line.

<div class="language-text line-numbers-mode">

``` text
debug1: userauth-request for user root service ssh-connection method publickey [preauth]
debug1: attempt 1 failures 0 [preauth]
debug2: input_userauth_request: try method publickey [preauth]
debug2: userauth_pubkey: valid user root querying public key rsa-sha2-512 AAAAB3Nz[..SNIP TEST KEY..]
debug1: userauth_pubkey: test pkalg rsa-sha2-512 pkblob RSA SHA256:dzzMNRySEXAMPLE_VALUE72k4eXoLXXikQw [preauth]
Error checking authentication key RSA SHA256:dzz-Thisisanexamplekey-sI08R-EXAMPLE_VALUE-XXikQw in revoked keys file /etc/ssh/sshd_revoked_keys: No such file or directory
Failed publickey for root from 127.0.0.1 port 55986 ssh2: RSA SHA256:dzz-Thisisanexamplekey-sI08R3Mj72k4eXoLXXikQw
debug2: userauth_pubkey: authenticated 0 pkalg rsa-sha2-512 [preauth]
```

</div>

On the client side there is no indication of this, other than the private key offered failing and it falling through to other authentication methods, by default that will be `password`.

## How to configure Key Revocation

### If not using revocation currently

If you are not using key revocation, or if you are not using the [binary KRL format](https://man.openbsd.org/ssh-keygen.1#KEY_REVOCATION_LISTS), then you can add the keys to be revoked in the format of â€œ[Keys may be specified as a text file, listing one public key per line](https://man.openbsd.org/sshd_config#RevokedKeys)â€?.

<div class="language-text line-numbers-mode">

``` text
root@f00:/# cat <<EOF >>/etc/ssh/sshd_revoked_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDIYyJEjQCLgNImBIHMr1S91Rm3YXBb1cfZ/Cf6l6aN06fvhLM1fFzTy3ms0bBttsLAak0S44a2uv3XzanAzgOAcopWGjHTR6VRkgQMG4XJlj6MCMISlQGr8JDFXtF4q8QCAujD7LRMGjqkbFKtd8I+h4QBZFNMl2tPF1ReKvDDnhSzwlqHvcEx5Q11un3JszKeGwY4n/es7WKq+pGWc2RfyS5pGQNWfGpp8TiDtycV3F0wh0T0XQzAx7DaJolfbL4iyg5hsfPBBsN+slXYaZEh88V1gXoJb/us/ZnAue3/tpmMRC9FAQQyFVT2mR6LMz+YGRMU4QK6oe1OFmhXS8ZFH6EnFmV0RIR3H1MJnYvDUFsotC6z2F2Tf9TiV3OV3EChOoa2KN0pLTwYPNm6unwDaoFmaH27V+HGhbS8KkPIcie2E5ElMtI3xZ2Tc/+i/VjRRihWi1vNSEYS3+7/QjFVy8pVnBzyOlkHMVOBxhpNBthxlJCc76xuWPSLKWMSXDnNvzceayUk/nQzsSnQAh/3NL9L1WH/1FL/uZE89E/cVbdZUTtCsQ4syxEWWP0jQBCrrsuorAr+9yFAhqrQikm/OUHQNxa2WoMKosGoqs1Q5sDBEs2C/2r08gTmaR96AIWT3Lhru9ZZ7qUhkDDfsvy+PBx5/4lcmEZdoezZFbQspQ== rundeck@435cc7c0ec97
EOF
```

</div>

You *do not* have to restart `sshd` upon changing this file, as it is read per authentication cycle, as opposed to at startup.

### Using revocation currently

If you are using [sshâ€™s binary KRL format](https://man.openbsd.org/ssh-keygen.1#KEY_REVOCATION_LISTS) then you can revoke the keys with the following

Make sure you are using KRL currently.

<div class="language-text line-numbers-mode">

``` text
root@f00:~# file /etc/ssh/sshd_revoked_keys
/etc/ssh/sshd_revoked_keys: OpenSSH key/certificate revocation list, format 1, version 0, generated Wed Jul 19 22:12:29 2021

root@f00:~# ssh-keygen -Q -l -f /etc/ssh/sshd_revoked_keys
# KRL version 0
# Generated at 20210719T221208
```

</div>

If this file does not currently exist, or is empty, you can create it with [`ssh-keygen`](https://man.openbsd.org/ssh-keygen.1#k). *This will overwrite any file currently there!*

<div class="language-text line-numbers-mode">

``` text
root@f00:~# test -s /etc/ssh/sshd_revoked_keys ||  ssh-keygen -k -f /etc/ssh/sshd_revoked_key
```

</div>

To add keys to the KRL specify a file containing the public keys in question.

<div class="language-text line-numbers-mode">

``` text
root@f00:~# ssh-keygen -k -u -f /etc/ssh/sshd_revoked_keys rundecks.pub
Revoking from ./rundecks.pub

root@f00:~# ssh-keygen -Q -l -f /etc/ssh/sshd_revoked_keys
# KRL version 0
# Generated at 20220413T111508

hash: SHA256:SHA256:HyLeewEXAMPLE-KEY-VALUE613XsRXbFQd6nxU6ikdmcn0 # ssh-rsa
hash: SHA256:SHA256:fm4RAHEXAMPLE-KEY-VALUEwdGMeZcp7fIF5WjN015/3CA # ssh-rsa
```

</div>

To verify they are revoked, you can use the [`-Q`](https://man.openbsd.org/ssh-keygen.1#Q) function again, on each public key.

<div class="language-text line-numbers-mode">

``` text
root@f00:~# while read -r pubkey; do tmp="$(mktemp)" && echo "$pubkey" >"$tmp" && ssh-keygen -Q -f /etc/ssh/sshd_revoked_keys "$tmp" ; rm "$tmp" ; done <rundecks.pub
/tmp/tmp.r9tvLwOQia (rundeck@435EXAMPLE0ec97): REVOKED
/tmp/tmp.CzOPq3w9tq (rundeck@a940EXAMPLE34cf): REVOKED
```

</div>
