# Setup crypted repository
## Installation
### Git-crypt Installation
1. Ubuntu
    ```
    sudo apt update
    sudo apt install git-crypt
    ```
2. Windows
    TODO
### GPG Installation
1. Ubuntu
    ```
    sudo apt update
    sudo apt install gpg
    ```
2. Windows
    TODO
## Creation GPG Key
1. Ubuntu
    ```
    gpg --full-generate-key
    ```
    > Configuration:
    Kind of key: RSA and RSA
    Key long: 4096 bits
    Key valid duration: does not expire
    Real name: YOUR_NAME
    Email address: YOUR_EMAIL_ADDRESS
    Comment: SOME_COMMENT
    
    ```
    gpg --armor --export --output PUB_KEY_NAME KEY_HASH
    ```
    
    > Note:
    Now you have public gpg key as a file and you can share it
2. Windows
    TODO
        
## Setup repository encryption
1. Ubuntu
    - Open terminal and move to repository dictionary
        > Note: for this repository dictionary will be 'gpg-crypted-rep'
    
    - Initialize git-crypt
        ```
        git-crypt init
        ```
    - Open or create '.gitattributes' file and add the necessary files for encryption
        ```
        filename1.txt filter=git-crypt diff=git-crypt
        filename2.txt filter=git-crypt diff=git-crypt
        ```
    
### Adding collaborator
1. Ubuntu
    Before adding the collaborator you need to double check that you have been added to colloborators
    Once it done, please tell potential collaborator to create himself GPG key ([Creation GPG Key](#creation-gpg-key))
    Then this user should send you public key
    Once you get it, you need import it to your key list
    ```
    gpg --import-key PUBLIC_KEY_FILE_NAME
    ```
    Then we need mark this key as trusted, find hash of imported key (or user email specified for this key)
    ```
    gpg --edit-key HASH_OR_EMAIL_COLLABORATOR_KEY
    ```
    Type `trust`
    > Note:
    How far you trust this key: 5 (I trust ultimately)
    Do you rellay want to set this key to ultimate trust: yes
    
    Type `save` to exit from key editing
    Now move to repository dictionary and add new gpg user
    ```
    git-crypt add-gpg-user HASH_OR_EMAIL_COLLABORATOR_KEY
    ```
    Last thing is commit changes that made by `git-crypt` and push them to remote repository
    Now collaborator can see encrypted files if him still can't type `git-crypt unlock`
