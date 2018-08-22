Git
===

## Using multiple git accounts on OSX

It can be a pain to use multiple git accounts on OSX, as simply adding the multiple SSH keys is not enough. 
When performing actions that checks the user's permissions (push, etc.), git will stop at the first key it finds in the ssh-agent.
This is problematic if this is not the key related to the account you want to use for the repository you are currently working on.

To solve this problem, a simple solution can do the trick. The main idea is to associate an SSH key with a virtual host.
This can be done by adding a `config` file in the `~/.ssh` folder which will pair the keys with the hosts like so (here an example with work/home accounts):

    Host *
      UseKeychain yes
      AddKeysToAgent yes
    
    # Personal GitHub account:
    Host home-github.com
      HostName github.com
      User git
      IdentityFile ~/.ssh/github_home
      IdentitiesOnly yes
    
    # Work GitHub account:
    Host work-github.com
      HostName github.com
      User git
      IdentityFile ~/.ssh/github_work
      IdentitiesOnly yes

The main step required for this to work is now to checkout every repository using one of these virtual hosts. E.g. at work, one should do: 

    git clone git@work-github.com:Company/repository.git
                  ^^^^^

Note though that an extra step is needed to make this properly: setting the user name and email for the repository. This should be done for each repository in theory.
In practice, the simplest solution is to keep the main user informations as a global git configuration, i.e. with:

    git config --global user.email "someone@work.com"

Then, set up the least used user infos for specific repository:

    git config --local user.email "someone@home.com"

And that's it.
