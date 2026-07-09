# Con/boarding

This pages is intended for new employees of the Center for Open Neuroscience.
Please note that some of the following links and resources are not publicly accessible.

## Accounts

### GitHub

1. Ask Yarik to add you to the [CON Org](https://github.com/con), including possibly the 'centroids' team.

1. Add yourself to [whoweare](https://github.com/con/centerforopenneuroscience.org/blob/master/content/pages/whoweare.html) to be displayed on [the website](https://centerforopenneuroscience.org/whoweare).



#### Conventions

1. Use `https` instead of `ssh` for git remotes to make the configuration
   more portable. You can switch to `ssh` for pushing by appending to your
   `~/.gitconfig`

   ```
   [url "git@github.com:"]
      pushinsteadOf = https://github.com/
      pushinsteadOf = http://github.com/
   [url "git@gitlab.com:"]
      pushInsteadOf = https://gitlab.com/
   [url "git@bitbucket.org:"]
      pushinsteadOf = https://bitbucket.org/
   ```
1. While you are modifying `~/.gitconfig` you might consider setting your
   default branch as well.

   ```
   [init]
      defaultBranch = main
   ```

1. Use standard commit messages, see [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/#summary).
   (Also see [DataLad's commit conventions](https://github.com/datalad/datalad-core/blob/main/CONTRIBUTING.md#conventional-commits)

1. Follow [REUSE Software spec](https://reuse.software/spec-3.3/) to ensure that licenses and
   copyright information are "comprehensive, unambiguous, human- and machine-readable".

## Chat clients

CON does not currently have a centralized IM infrastructure, there are however a number of per-project channels.

0. CON-internal: by invitation (ask a colleague for the URL) after registering on [matrix.to](https://matrix.to).
1. DANDI slack workspace: registration comes with registering a user on https://dandiarchive.org. Then user needs to be invited to "internal" room.
2. ReproNIM slack workspace (ask Yarik)
3. DataLad matrix.io: [public room](https://matrix.to/#/#datalad:matrix.org), [internal](not-sure-if-not-private)
4. [NWB slack workspace](https://join.slack.com/t/nwb-users/shared_invite/enQtNzMwOTcwNzQ2MDM5LWMyZDUwODJjYjM3MzMzYzZiNDk4ZTU3ZjQ3MmMxMmY5MDUyNzc0ZDI5ZjViYmJjYTQ5NjljOGFjZmMwOGIwZmQ)
5. [mattermost brainhack](https://mattermost.brainhack.org/): for various open science projects

## Calendar

0. TODO: CON Calendar
1. [DANDI cal](https://calendar.google.com/calendar/embed?src=6a48akicfittlo932phrhdm84g%40group.calendar.google.com&ctz=America%2FNew_York)
1. [ReproNIM cal](https://calendar.google.com/calendar/embed?src=ahfj9rg32tmb459up8gkv2t7ek%40group.calendar.google.com&ctz=America%2FNew_York)
1. Datalad cal (I got a link for this but didn't have permissions, Yarik?)
1. [PBS Events Calendar](https://calendar.google.com/calendar/embed?src=c_31ckainhaqlmhk4hkc633fs9ho%40group.calendar.google.com&ctz=America%2FNew_York) (if you are local)

## Drive

1. [Repronim grant directory](https://drive.google.com/drive/folders/1AbpaqrCnInU-0V7KCxIn0RdG7578JrzI?ths=true)

## Compute

#### CON's development boxes

Among others:
- `smaug`: lots of storage for home directories, aging with limited RAM.
- `typhon`: beefy compute available including GPU compute, storage on `/data/<username>`.


1. Send desired login name and the `.pub` portion of your preferred SSH key to Yarik for
   development box(es): `smaug`, `typhon`, `drogon`, etc.

2. Set the connection details:

   ```
   export CON_SSH_KEY="$HOME/.ssh/YOUR_KEY" CON_SSH_USER="YOUR_USERNAME" CON_SSH_PORT="YOUR_PORT"
   ```

3. Use `ssh-agent` for your private key:

   ```
   ssh-add -t 36000 "$CON_SSH_KEY"
   ssh-add -l # display the fingerprint of the key
   ```

4. Consider using the following command to append the host entries to your SSH
   config file:

   ```
   cat >> ~/.ssh/config <<EOF
   Host smaug smaug.datalad.org smaug.dartmouth.edu
       HostName smaug.dartmouth.edu
       User $CON_SSH_USER
       Port $CON_SSH_PORT
       IdentityFile $CON_SSH_KEY
       IdentitiesOnly yes
       ForwardAgent yes
       PasswordAuthentication no

   Host typhon typhon.datalad.org typhon.dartmouth.edu
       HostName typhon.dartmouth.edu
       User $CON_SSH_USER
       Port $CON_SSH_PORT
       IdentityFile $CON_SSH_KEY
       IdentitiesOnly yes
       ProxyJump smaug
       ForwardAgent yes
       PasswordAuthentication no

   Host drogon drogon.datalad.org drogon.dartmouth.edu
       HostName drogon.dartmouth.edu
       User $CON_SSH_USER
       Port $CON_SSH_PORT
       IdentityFile $CON_SSH_KEY
       IdentitiesOnly yes
       ProxyJump smaug
       ForwardAgent yes
       PasswordAuthentication no
   EOF
   ```

   The options are:

   - `IdentityFile`: use the key you sent to Yarik.
   - `IdentitiesOnly yes`: avoid trying unrelated keys from your agent.
   - `ForwardAgent yes`: make your local agent available after logging into
     a remote host.
   - `ProxyJump smaug`: reach `typhon` and `drogon` through `smaug` as there accessibility is more limited.
   - `PasswordAuthentication no`: do not use SSH password authentication.

   Equivalent manual command for illustrative purposes:

   ```
   ssh -A -o PasswordAuthentication=no -o IdentitiesOnly=yes -i "$CON_SSH_KEY" -J "$CON_SSH_USER@smaug.dartmouth.edu:$CON_SSH_PORT" -p "$CON_SSH_PORT" "$CON_SSH_USER@typhon.dartmouth.edu"
   ```

   With this SSH config in place, `ssh typhon` etc. should work, connecting
   through `smaug` as required.

   Useful diagnostic:

   ```
   ssh -G typhon | grep -E '^(hostname|user|port|identityfile|proxyjump|passwordauthentication)'
   ```

5. If you need to use MacOS, ask Yarik to add your key to the Con Mac.
   Then you can add to your SSH config in `smaug` and login from there. Configuration example:

   ```
   Host conmac
     HostName datalads-imac2.kiewit.dartmouth.edu
     AddKeysToAgent yes
     Port 2223
     User yoh
   ```

#### Discovery Cluster

Get an account for the Discovery Cluster at Dartmouth and set up remote access to it
   1. [Apply for Discovery Account](https://rcweb.dartmouth.edu/accounts/index.php)
   1. Subscribe to the [Dartmouth Research Computing mailing list](https://eepurl.com/c_EWgz).
   1. [Get access](https://services.dartmouth.edu/TDClient/1806/Portal/KB/?CategoryID=17668) to the VPN.
   1. Example ssh config entry:

      ```
      Host discovery discovery.dartmouth.edu
          HostName discovery.dartmouth.edu
          PreferredAuthentications gssapi-with-mic,hostbased,keyboard-interactive,password
          ServerAliveInterval 30
          User <your user name at discovery>
      ```
   1. More information regarding the Discovery Cluster can be found at [its documentation](https://services.dartmouth.edu/TDClient/1806/Portal/KB/?CategoryID=21663)
      at Services Portal, [Dartmouth Brain Imaging Center Handbook](https://dbic-handbook.readthedocs.io/en/latest/discovery.html),
      and [John Hudson's course notes](https://rcweb.dartmouth.edu/~john/HPC/).
   1. Request `rc-DBIC` group from Yarik. (Necessary to use Datalad) Be sure to follow this guide to use DBIC-installed git-annex. https://dbic-handbook.readthedocs.io/en/latest/mri/dataaccess.html#discovery-filesystem

#### Using VNC

   To find out if a server provides VNC, try running `vncserver --version`. If the
   command returns information about a VNC server, VNC is available on the server.
   Once you have access to a server with VNC available, you can use VNC to access a
   desktop environment on the server by following these steps:
   1. Run `vncpasswd` to set a password to used for logging into VNC
      sessions (`man vncpasswd` for details)

      ```vncpasswd```
   2. Run `vncserver` to start a TigerVNC desktop session (`man vncserver` for details)

      ```vncserver```

      The started desktop session will be assigned an X display number that will be
      indicated in the output of the `vncserver` command.
   3. Each session is assigned a particular port number for network access. The port
      number is the X display number plus 5900. For example, if the X display number is
      1, the port number will be 5901. Running `vncserver -list` will show the X display
      number and port number for each existing VNC session.
   4. To connect to the VNC session from your local machine, you will need a VNC client.

      If are using `xtightvncviewer` which has builtin SSH tunneling, you can connect to
      a VNC session directly.

      ```xtightvncviewer -via <username>@<server name>.dartmouth.edu localhost:<VNC assigned port number>```

      If you are using a VNC client that does not have builtin SSH tunneling, you will
      need to create an SSH tunnel to the VNC server and then connect to the VNC session
      through the tunnel.

      1. Create an SSH tunnel to the VNC server

         ```ssh -L <local port number>:localhost:<VNC assigned port number> <username>@<server name>.dartmouth.edu```

      2. Connect to the VNC session through the SSH tunnel using the VNC client on your
         local machine at `localhost:<local port number>`

      Where `<VNC assigned port number>` is the port number assigned to the VNC session
      on the server and `<local port number>` is the port number on your local machine
      that you want to use for the SSH tunnel. `<server name>` is the name of the server
      where the VNC session is running.

#### Other resources

1. ReproNim: request iam from David for AWS Access
1. DANDI: request credentials for DANDI from Satra

## Collaboration on Pull Requests

The CON team works on many projects and is often spread thin, so its important to be efficient with pull requests and review.

### Creating PRs
- Keep PRs as small and focused as possible - this makes them easier for others to review and has a lower risk of introducing unintended side effects (a +/-  lines of code under 200 excluding docs/tests generally advised)
- Self-review your diff and PR before requesting review
- Mark as draft if not ready for review

### PR Description
- Link the appropriate issue at the start of the PR (and if within a list, github expands the issue title) using a [keyword phrase](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword) which will then automatically close the issue upon merge (you can also manually link them using the 'Development' tab on the right)
- Make sure the description explains why the change was made (and how/what, if helpful to reviewers)
- use `- [ ] todo item` to indicate remaining work

### Requesting Review
- Consider using an AI tool for initial review, and make sure to address or resolve/close the items of that review before inviting human reviewers.
- Invite others to review (even if they are not "experts" on that repo)

## Commit Co-Authorship

When an AI tool (agent, coding assistant, IDE integration) materially contributes to a commit, the commit MUST include a `Co-Authored-By` trailer identifying both the **tool and its version** and the **model and its version**. This makes the git history the inspectable provenance record so anyone reading the repo can tell which tool produced which change.

Format:

```
Co-Authored-By: <Tool> <tool-version> / <Model> <model-version> <noreply@<vendor-domain>>
```

Discover the tool version from the tool itself (commonly `--version`) and use the model identifier the tool reports. Don't guess.

### Encode this rule in your user-level and repo's AI instructions

Repo-level and user-level AI instruction files (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, etc.) should carry this rule so whichever AI tool is in use applies it automatically, without a human prompting each commit. Drop the following block into yours:

````markdown
## Commit co-authorship

Every commit you author MUST include a `Co-Authored-By` trailer identifying both your tool name + version and your underlying model + version. Format:

```
Co-Authored-By: <Tool> <tool-version> / <Model> <model-version> <noreply@<vendor-domain>>
```

Use the actual versions reported by your tool. Don't guess.
````

### Example: Claude Code

```
Co-Authored-By: Claude Code 2.1.63 / Claude Opus 4.6 <noreply@anthropic.com>
```

`claude --version` reports the Claude Code CLI version; the active model is reported by the CLI in its status / via `/model`.
