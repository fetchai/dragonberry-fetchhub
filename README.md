# Fetch.ai fetchd repository

This repository contains a fork of the `fetchd` application that has had the dragonberry security patch applied.

Due to the nature of the security vunerability, we want to keep information about this vunerability limited to a need to know basis. This effort is being coordinated across a number of other ecosystem chains.

- **Please DO NOT discuss this on group channels**
- **If you have questions or comments please contact members of the Fetch.ai team via Discord DM**

## Formal Disclosure

Shortly after this patch has been applied across the ecosystem, formal disclosures will begin. Ultimately this will mean that a `v0.10.7` upgrade will be released and will go through the formal governance proposal process.

# What to do now?

The patch is not consensus breaking (provided that the exploit has not been triggered). Therefore it is safe to upgrade your nodes.

We expect the majority of validators to be running `v0.10.5`, with some early adopters running `v0.10.6`. We have provided two versions of the patch for each of these cases.

To check which version you have run the following command:

```bash
fetchd version
```

## For nodes running `v0.10.5`

You may already have the fetchd repository on your machine from the previous installation. If not, you can:

```bash
git clone --branch v0.10.5+dragonberry.1 https://github.com/fetchai/dragonberry-fetchhub.git fetchd_0.10.5_dragonberry
cd fetchd_0.10.5_dragonberry
```

If you already have an existing clone, place yourself in and:

```bash
git remote add dragonberry git@github.com:fetchai/dragonberry-fetchhub.git
git fetch --all
git clean -fd
git checkout v0.10.5+dragonberry.1
```

Now you can install the new fetchd version:

```bash
make install

# and verify you now have the correct version:
fetchd -h
# must print fetchd help message

fetchd version
# must print v0.10.5+dragonberry.1
```

Make sure the version is correct before proceeding further!

You're now ready to restart your node.

## For nodes running `v0.10.6`

You may already have the fetchd repository on your machine from the previous installation. If not, you can:

```bash
git clone --branch v0.10.6+dragonberry.1 https://github.com/fetchai/fetchd.git fetchd_0.10.6_dragonberry
cd fetchd_0.10.6_dragonberry
```

If you already have an existing clone, place yourself in and:

```bash
git remote add dragonberry git@github.com:fetchai/dragonberry-fetchhub.git
git fetch --all
git clean -fd
git checkout v0.10.6+dragonberry.1
```

Now you can install the new fetchd version:

```bash
make install

# and verify you now have the correct version:
fetchd -h
# must print fetchd help message

fetchd version
# must print v0.10.6+dragonberry.1
```

Make sure the version is correct before proceeding further!

You're now ready to restart your node.

## Restarting fetchd

Fetchd can now be restarted. The exact commands depends on your particular setup (systemd, cosmovisor...)

After the restart the node should continue to produce blocks as normal.

## Verify upgrade completed

You can now query your local RPC endpoint to verify the right version is running and the node properly restarted:

```bash
curl -s http://localhost:26657/abci_info | jq -r '.result.response.version'

# should say either: v0.10.5+dragonberry.1 or v0.10.6+dragonberry.1
```

Make sure this prints `v0.10.5+dragonberry.1` or `v0.10.6+dragonberry.1`, if not, double check you're on the right git tag in the fetchd repository, that the `make install` didn't produce errors, and that your properly restarted your node.

## Notify the Fetch.ai Team

Please message ejfitzgerald#6094 directly on discord to let the Fetch.ai team know when you have completed this upgrade or if you have run into any problems.
