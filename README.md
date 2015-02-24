
# what
just an handy, Vagrantfile for transient linux tasks, with a
plugable and persistent home directory.

# notes
- this **only makes sense if you are using OS X as the host**.
- fedora (20) based. you like it or you hate it
- Parallels specific, as it is what i use here
- actual provisioning is done via Ansible (see under
  [provisioning/](./provisioning) for details).
- built-in *ssh* and *X-Windows* passthrough.
  - for *ssh* passthrough to behave make sure that you have in your **host**
  running shell profile (*~/bash_profile*, *~/.zshrc*, whatever) something
  along ...

     ```sh
        if ! ssh-add -l &> /dev/null; then
            ssh-add ~/.ssh/id_rsa &> /dev/null
        fi

     ```
  - for some keyboard key combinations (say **Ctrl-Alt-Del**) to *walk* smoothly
  end-to-end you'll need to have in your *host* in **~/.Xmodmap**

    ```
       clear Mod1
       keycode 66 = Alt_L
       keycode 69 = Alt_R
       add Mod1 = Alt_L
       add Mod1 = Alt_R
     ```

- by default the **non transient** data directory is **persistent/** in the same
  folder as the Vagrantfile. To change it point the desired location into the
  **PERSISTENT_HOMEDIR** shell variable *before* invoking ```vagrant up```

# licensing
[CC0 1.0 Universal](LICENSE)

