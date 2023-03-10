## Git SSH config

1. Generate

    ```
    ssh-keygen -t ed25519 -C "your_email@example.com" -f "key_filename"
    ```

    ```
    ssh-keygen -t ed25519 -C "github - xe" -f "github-xe"
    ```

2. Start agnet

    ```
    eval "$(ssh-agent -s)"
    ```

3. Add keys to agent

    ```
    ssh-add ~/.ssh/key_filename
    ```

    - for mac:
        ```
        ssh-add -K ~/.ssh/key_filename
        ```

        -K - store passphrase for private key in Keychain
    
    list loaded keys:

    ```
    ssh-add -l
    ```

4. Create config

    `~/.ssh/config`
    ```
    Host github.com-xe
        HostName github.com
        User git
        IdentityFile ~/.ssh/github-xe
        IdentitiesOnly yes

    Host github.com-dc
        HostName github.com
        User git
        IdentityFile ~/.ssh/github-dc
        IdentitiesOnly yes
    ```

    - for mac add to each entry:
        ```
        UseKeychain yes
        AddKeysToAgent yes
        ```

5. Add keys to site or host

    - win
        ```
        cat ~\.ssh\key_filename.pub | clip
        ```
    - mac
        ```
        cat ~\.ssh\key_filename.pub | pbcopy
        ```

    ```
    ssh-copy-id -i ~/.ssh/key_filename.pub user@host
    ```

6. Test

    ```
    ssh -T git@github.com-xe
    ssh -T git@github.com-dc
    ```

