# Con/boarding

This pages is intended for new employees of the Center for Open
Neuroscience, so please note that the public does not have access to
some of these links.

## Accounts

### Github

Ask Yarik to add you to the [CON Org](https://github.com/con)

### Chat clients

No CON centralized IM ATM, only per project and for different communities.

0. CON-internal: by invitation (ask someone for a URL) after you get on matrix.io.
1. DANDI slack workspace: registration comes with registering a user on https://dandiarchive.org. Then user needs to be invited to "internal" room.
2. ReproNIM slack workspace (ask Yarik)
3. DataLad matrix.io: [public room](https://matrix.to/#/#datalad:matrix.org), [internal](not-sure-if-not-private)
4. [NWB slack workspace](https://join.slack.com/t/nwb-users/shared_invite/enQtNzMwOTcwNzQ2MDM5LWMyZDUwODJjYjM3MzMzYzZiNDk4ZTU3ZjQ3MmMxMmY5MDUyNzc0ZDI5ZjViYmJjYTQ5NjljOGFjZmMwOGIwZmQ)
5. [mattermost brainhack](https://mattermost.brainhack.org/): for various open science projects

### Calendar

0. TODO: CON Calendar
1. [DANDI cal](https://calendar.google.com/calendar/embed?src=6a48akicfittlo932phrhdm84g%40group.calendar.google.com&ctz=America%2FNew_York)
2. [ReproNIM cal](https://calendar.google.com/calendar/embed?src=ahfj9rg32tmb459up8gkv2t7ek%40group.calendar.google.com&ctz=America%2FNew_York)
2. Datalad cal (I got a link for this but didn't have permissions, Yarik?)

### Drive

1. [Repronim grant directory](https://drive.google.com/drive/folders/1AbpaqrCnInU-0V7KCxIn0RdG7578JrzI?ths=true) 

### Compute

What are the appropriate uses of each box?
How much does it cost to run things?


1. Send desired login name and .pub portion of the SSH key to Yarik for development box(es): smaug, typhon, etc
2. Get an account for the Discovery Cluster at Dartmouth and set up remote access to it
   1. [Apply for Discovery Account](https://rcweb.dartmouth.edu/accounts/index.php)
   2. The Discovery Cluster can be accessed off campus either via VPN or ProxyJump through ssh.
      1. To set up VPN, please visit [the Services Portal](https://services.dartmouth.edu/TDClient/1806/Portal/KB/?CategoryID=17668) for info.
      2. To set up ProxyJump through ssh, you must already have ssh access to a server on campus.
         * For example, if you already have ssh access to our server `Smaug`, you can set up ProxyJump by adding the following to your `~/.ssh/config` file:
         ```
            Host smaug smaug.dartmouth.edu
                Hostname smaug.dartmouth.edu
                AddKeysToAgent yes
                IdentityFile <path to your private key>
                port <ssh port for Smaug>
                user <your username>
         
            Host discovery discovery.dartmouth.edu
                HostName discovery.dartmouth.edu
                ProxyJump smaug.dartmouth.edu
                ServerAliveInterval 30
                GSSAPIAuthentication yes
                GSSAPIDelegateCredentials yes
                user <your user name at discovery>
         ```
   3. More information regarding the Discovery Cluster can be found at [its documentation](https://services.dartmouth.edu/TDClient/1806/Portal/KB/?CategoryID=21663) 
      at Services Portal, [Dartmouth Brain Imaging Center Handbook](https://dbic-handbook.readthedocs.io/en/latest/discovery.html),
      and [John Hudson's course notes](https://rcweb.dartmouth.edu/~john/HPC/).
                
3. ReproNim: request iam from David for AWS Access
4. DANDI: request credentials for DANDI from Satra



### Boilerplate

1. Add yourself to [whoweare](https://github.com/con/centerforopenneuroscience.org/blob/master/content/pages/whoweare.html) to be displayed on [the website](https://centerforopenneuroscience.org/whoweare).


