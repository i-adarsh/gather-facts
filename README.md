# Chandu Milestone


## 1st Milestone

>1. Create User  ```https://github.com/i-adarsh/create-user```
>
> This role is used to create multiple users on the remote server with the provided group name.
```
  roles:
          - role: create-user
            service_account_name: appadm          
            owner_username: appadm
            owner_groupname: apps
            service_account_username_uid: 504
            service_account_groupname_gid: 504
            owner_username_home: /home/{{ owner_username }}
            owner_username_shell: /bin/bash
            ignore_unreachable: yes
```
> 
>   
>
>2. Create Directory ```https://github.com/i-adarsh/create-dir```
>
>This role is used to create multiple directories on the remote server with provided name and permissions.
>
```
  - role: create-dir
    with_items: 
          - "{{ dir_inf }}"
          - "{{ common_dir_info }}"


Used Variables
        dir_inf:
            - dir_path: /files
              dir_owner: jboss
              dir_group: jboss
              dir_mode: '0755'

        common_dir_info:
            - dir_path: "/java/openjava16"
            - dir_path: "/java/openjava14"
            - dir_path: "/java/openjava15"
            - dir_path: "/java/oraclejava16"
            - dir_path: "/java/oraclejava14"
            - dir_path: "/java/oraclejava15"
            - dir_path: "/jboss/jboss-7.4"
            - dir_path: "/jboss/jboss-7.1"
            - dir_path: "/jboss/jboss-7.3"
        dir_owner: jboss
        dir_group: jboss
        dir_mode: '0755'
```
>3.	File Encrypt ```https://github.com/i-adarsh/file-encrypt```
>
>This role is used to encrypt the provided file.
>
```
- name: Encrypting Files
  gather_facts: no
  hosts: localhost
  roles:
          - role: create-vault
            files:
                - file_to_encrypt: test/foo.yml
                  password_file: password
            ignore_unreachable: yes
```
>4.	String Encrypt ```https://github.com/i-adarsh/string-encrypt```
>
>This role is used to encrypt the provided string and save into the destination file.
```
- name: Encrypting String
  gather_facts: no
  hosts: localhost

  roles:
          - role: string-encrypt
            encryption:
                - password_file: "password"
                  string_to_encrypt: "test3"
                  name_of_variable: "value3"
                  file_name: "test/bar.yml"

                - password_file: "password"
                  string_to_encrypt: "test4"
                  name_of_variable: "value4"
                  file_name: "test/bar.yml"
            ignore_unreachable: yes
```
#
## 2nd Milestone

>1. Installing JBoss  ```https://github.com/i-adarsh/install-jboss```
>
> This role is used to install multiple versions of JBoss on the remote server.
```
      - role: install-jboss
        # Variables are defines below . . .
        jboss_eap_download_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.3.0.zip
        jboss_eap_download_dir: /files
        jboss_eap_zip_file: jboss-eap-7.3.0.zip
        jboss_eap_library_dest: /jboss
        jboss_eap_jboss_home: /jboss
        jboss_eap_dir_name: jboss-eap-7.3 # Name of the folder after extracting the zip file
        jboss_eap_user: jboss
        jboss_eap_group: jboss
        ansible_env.PATH: JBOSS_HOME
        jboss_eap_home: /jboss/jboss
        jboss_eap_mode: 0755
```
> 
>   
>
>2. Patching JBoss ```https://github.com/i-adarsh/apply-jboss-patch```
>
>This role is used for patching of JBoss to the newer version. 
>
```
      - role: apply-jboss-patch
        jboss_eap_download_dir: /files
        jboss_eap_patch_file: jboss-eap-7.3.6-patch.zip # Path of your ZIP file
        jboss_eap_patch_file_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.3.6-patch.zip
        jboss_eap_jboss_home: /jboss/jboss/
        jboss_eap_home: /jboss/jboss
        jboss_eap_user: jboss
        jboss_eap_patch: yes 
        jboss_eap_patch_dest: /files/jboss-eap-7.3.6-patch.zip
        jboss_eap_patch_artifact_name: jboss-eap-7.3.6-patch.zip
```

#
## 3rd Milestone

>1. Installing Java  ```https://github.com/i-adarsh/install-java```
>
> This role is used to install multiple versions of java i.e. oracle JDK and open JDK on the remote server.
```
- role: install-java
        open_jdk_details:
          - open_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/openjdk-16.0.1_linux-x64_bin.tar.gz
            open_jdk_download_dir: /files
            open_jdk_file: openjdk-16.0.1_linux-x64_bin.tar.gz
            open_jdk_library_dest: /java/openjava16
        
          - open_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/openjdk-14_linux-x64_bin.tar.gz
            open_jdk_download_dir: /files
            open_jdk_file: openjdk-14_linux-x64_bin.tar.gz
            open_jdk_library_dest: /java/openjava14

          - open_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/openjdk-15_windows-x64_bin.zip
            open_jdk_download_dir: /files
            open_jdk_file: openjdk-15_windows-x64_bin.zip
            open_jdk_library_dest: /java/openjava15

        oracle_jdk_details:
          - oracle_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/jdk-16.0.1_linux-x64_bin.tar.gz
            oracle_jdk_download_dir: /files
            oracle_jdk_file: jdk-16.0.1_linux-x64_bin.tar.gz
            oracle_jdk_library_dest: /java/oraclejava16 # Name where tar file get extracted

          - oracle_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/jdk-14.0.2_linux-x64_bin.tar.gz
            oracle_jdk_download_dir: /files
            oracle_jdk_file: jdk-14.0.2_linux-x64_bin.tar.gz
            oracle_jdk_library_dest: /java/oraclejava14

          - oracle_jdk_download_url: https://ongraphtechnologies.s3.amazonaws.com/openjdk-14_windows-x64_bin.zip
            oracle_jdk_download_dir: /files
            oracle_jdk_file: openjdk-14_windows-x64_bin.zip
            oracle_jdk_library_dest: /java/oraclejava15 

        jdk_user: jboss
        jdk_group: jboss
        jdk_mode: 0755
```
> 
>   
>
>2. Multiple JBoss Install ```https://github.com/i-adarsh/multi-install-jboss```
>
>This role is used for multiple patching of JBoss Versions.
>
```
      - role: multi-install-jboss
        jboss_eap_details:
          - jboss_eap_download_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.3.0.zip
            jboss_eap_download_dir: /files
            jboss_eap_zip_file: jboss-eap-7.3.0.zip
            jboss_eap_dir_name: jboss-eap-7.3
            jboss_eap_extract_dest: /jboss
            jboss_eap_library_dest: /jboss/jboss-7.3/
          
          - jboss_eap_download_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.1.0.zip
            jboss_eap_download_dir: /files
            jboss_eap_zip_file: jboss-eap-7.1.0.zip
            jboss_eap_dir_name: jboss-eap-7.1
            jboss_eap_extract_dest: /jboss
            jboss_eap_library_dest: /jboss/jboss-7.1/

          - jboss_eap_download_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.4.0.zip
            jboss_eap_download_dir: /files
            jboss_eap_zip_file: jboss-eap-7.4.0.zip
            jboss_eap_dir_name: jboss-eap-7.4
            jboss_eap_extract_dest: /jboss
            jboss_eap_library_dest: /jboss/jboss-7.4/

        jboss_eap_user: jboss
        jboss_eap_group: jboss
        jboss_eap_mode: 0755
```

#
## 4th Milestone

>1. Dynamic script for patching  ```https://github.com/i-adarsh/Chandu-Milestone-4```
>
> This role is used for multiple patching of JBoss through the script.
```
   # Scipt Patching
   - role: jboss-patch-script
     with_items:
       - "{{ patch_details }}"

# Provide any different (random name) patch_name for different patching versions
patch_details:
  - jboss_eap_patch_artifact_name: jboss-eap-7.3.6-patch.zip
    jboss_eap_user: jboss
    java_path: /java/oraclejava8/jdk1.8.0_291/
    jboss_bin: /jboss/jboss-7.3/bin/
    patch_name: patch1
    jboss_eap_patch_file_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.3.8-patch.zip
    jboss_eap_download_dir: /files
```
> 
>   
>
>2. Multiple JBoss Patch 
>
>This role is used for multiple patching of JBoss Versions.
>
```
# Patching JBoss
      - role: run-multi-patch
        with_items:
          - "{{ jboss_eap_patch_details }}"

# ========== 1st Patch Vars ==========
jboss_eap_patch_details:
  - jboss_eap_download_dir: /files
    jboss_eap_user: jboss
    jboss_eap_patch_file: jboss-eap-7.3.6-patch.zip # Path of your ZIP file
    jboss_eap_patch_file_url: https://ongraphtechnologies.s3.amazonaws.com/jboss-eap-7.3.6-patch.zip
    jboss_eap_jboss_home: /jboss/jboss-7.3
    jboss_eap_home: /jboss/jboss-7.3
    jboss_eap_patch_dest: /files/jboss-eap-7.3.6-patch.zip
    jboss_eap_patch_artifact_name: jboss-eap-7.3.6-patch.zip
    java_home: /java/oraclejava8/jdk1.8.0_291/
```

#
## 5th Milestone

>1. Ansible logs get created and appended after each playbook run. ```https://github.com/i-adarsh/Milestone-5```

## Contributers
>[Adarsh Kumar](https://github.com/i-adarsh)


## License
[MIT](https://choosealicense.com/licenses/mit/)
