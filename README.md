# Nextcloud docker-client
This image provides you an alpine based image for syncing your files with a remote [nextcloud server ](https://nextcloud.com/)

[![](https://images.microbadger.com/badges/image/juanitomint/nextcloud-client.svg)](https://microbadger.com/images/juanitomint/nextcloud-client "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/juanitomint/nextcloud-client.svg)](https://microbadger.com/images/juanitomint/nextcloud-client "Get your own version badge on microbadger.com")


This image is based on the work made by: [Martin Peters](https://github.com/FreakyBytes)

## Example using local folder

    docker run -it --rm \
      -v $(pwd)/sync-folder:/media/nextcloud \
      -e NC_USER=$username -e NC_PASS=$password \
      -e NC_URL=$server_url\
      juanitomint/nextcloud-client

## Example using local folder and exclude settings. You have to place a "exclude" file and a "unsyncfolders" file into one directory and mount it into the docker container

    docker run -it --rm \
      -v $(pwd)/sync-folder:/media/nextcloud \
      -v /path/to/settingsfolder:/settings \
      -e NC_USER=$username -e NC_PASS=$password \
      -e NC_URL=$server_url\
      juanitomint/nextcloud-client

## Example for the file "exclude" in the settings folder

    file1
    file2

## Example for the file "unsyncfolders" in the settings folder

    folder1
    folder2

## Example using a [named volume](https://docs.docker.com/storage/volumes/)

    docker run -it --rm \
      -v some_named_volume:/media/nextcloud \
      -e NC_USER=$username -e NC_PASS=$password \
      -e NC_URL=$server_url\
      juanitomint/nextcloud-client

## Example one time run

    docker run -it --rm \
      -v some_named_volume:/media/nextcloud \
      -e NC_USER=$username -e NC_PASS=$password \
      -e NC_URL=$server_url\
      -e NC_EXIT=true\
      juanitomint/nextcloud-client



replace:
 * $username
 * $password 
 * $server_url 
 
 with valid values for an existing and valid user on a Nextcloud Server.

## ENV variables to customize your deploy

##### NC_URL
URL to the Nextcloud instance. You can sync spepcific folders by providing the full path in the URL like `https://cloud.example.com/remote.php/webdav/<path/to/custom/dir>`. This will only sync the contents of `path/to/custom/dir`.

##### NC_USER
The user name to log in
Default: username
##### NC_PASS 
Valid password for the user above in clear text
Default: password

##### NC_SOURCE_DIR
The directory inside de docker container to be synced, usually you will have a local mount here or a named volume
default: /media/nextcloud/

##### NC_SILENT
whether or not output activity to console
default: false

##### NC_INTERVAL
Sets the interval between syncs in seconds
default: 300 (300 /60 = 5 Minutes)

##### NC_EXIT
If "true" the sync will happen once and then the container will exit, very usefull for using 
in conjunction with cron or schedulers
default: false
example: 
## Advanced settings

##### USER
The system user inside the container you want to use for runing the sync

default: ncsync

##### USER_GID
The system user group id inside the container you want to use for runing the sync

default: 1000

##### USER_UID
The system user id inside the container you want to use for runing the sync

default: 1000

##### NC_TRUST_CERT
whether or not trust self signed certificates or invalid certificates

default: false

##### NC_HIDDEN
whether or not nextcloud should be forced to sync hidden files

default: false


Any comment or propblem feel free to [fill an issue](https://github.com/juanitomint/nextcloud-client-docker/issues/new) or make a PR!

