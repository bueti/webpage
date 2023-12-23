---
title: Bocker - Backup and Restore in Docker
summaryImage: "logo.png"
keepImageRatio: true
tags: [ "blog" ]
summary: I wrote a tool that puts a backup into a Docker image and stores it on a private repo in Docker Hub.
hideLastModified: true
---

A few years ago I had a problem. When I was working on iOverlander I realized that there wasn't an automated PostgreSQL database backup. This was a problem because the database changes very frequently.  Thousands of users are creating new Points of Interest and upload check-ins daily and they are all stored in a PostgreSQL database. This is the core of iOverlander, thus having a backup is kinda important.

I created a small script that takes a backup. But now the question is where do you store the backup?
Of course, you could store it on an S3 compatible storage but then you have to set this up and pay for the storage you use (one database backup was about 800MiB).
But maybe there's a simpler and free way to store a backup at a safe place?

In comes Docker Hub! I already pay for a Docker Hub account to have private repository. As far as I know there are no restrictions on how many images / repositories you can have and as long as your image is smaller than 10GiB you shouldn't run into any problems.

So why not wrap the backup in a Docker image and push it to the private repository?! 
I hacked together a shell script that uses pg_dump to create backup file, creates a Docker image and pushes it to Docker Hub.
So far, so good.

The next problem is to actually use this backup and restore the database. Since the backup file is in a layer of the Docker image, it's a bit more complex and you first need to find the right layer and then extract the file. I never came around to write a script for that (and we never had to restore our production database). But whenever another volunteer needed to restore dump locally, I usually had to send them the file or explain the different steps needed to extract the backup from the image.

The other day I messed up my local iOverlander database and I had to restore it. It's been months since I had done this and I didn't quite remember all the steps.  Even though the documentation I wrote wasn't too bad, it still took me way too long to restore the database.

And so I decided to ditch the Shell script and write a CLI tool in Go to encode the whole process and so "BockeR -- Backup and Restore in Docker" was born.

I don't think this is gonna be useful for a lot of people, but it is a fun project which helped me learn writting Go code. I have many ideas for improvements and might implement some of them in the future (for example, use the Docker SDK instead of the docker cli).

If you are interested you can install bocker via my Homebrew:
{{< code language="shell" >}}
brew install bueti/tap/bocker
{{< /code >}}

Or
{{< code language="shell" line-numbers=false >}}
brew tap bueti/tap
brew install bocker
{{< /code >}}

or download the binary on Github: https://github.com/bueti/bocker/releases

How does it work? Pretty simple:
{{< codeWide language="shell" line-numbers=false >}}
$ bocker --help
Bocker is a command line tool which creates a backup from a PostgreSQL database, 
wraps it in a Docker image, and uploads it to Docker Hub. 
Of course, Bocker will also do the reverse and restore your database from a backup in Docker Hub.

Usage:
  bocker [command]

Available Commands:
  backup      Backup a Postgresql Database
  completion  Generate the autocompletion script for the specified shell
  help        Help about any command
  restore     Restores a Posgres database

Flags:
  -c, --container-id string   ID of container running PostgreSQL
  -d, --db-name string        Database name
  -h, --help                  help for bocker
  -n, --namespace string      Docker Namespace (default "bueti")
  -r, --repository string     Docker Repository

Use "bocker [command] --help" for more information about a command.
{{< /codeWide >}}

Example Backup:
{{< codeWide language="shell" line-numbers=false >}}
deployer@staging:~$ ./bocker backup -c 491d8559477c -s ioverlander_development -r ioverlander_backup -u ioverlander
INFO	2023/02/05 15:59:41 Creating backup...
INFO	2023/02/05 16:01:22 Building image...
INFO	2023/02/05 16:01:43 Pushing image...
Published image bueti/ioverlander_backup:2023-02-05_15-59-41
{{< /codeWide >}}

Example Restore:
{{< codeWide language="shell" line-numbers=false >}}
$ bocker restore -c a16952e2d855 -o ioverlander -t ioverlander_development \
    -s ioverlander_development -r ioverlander_backup --tag 2023-02-05_15-59-41
INFO    2023/02/05 17:14:26 Pulling image (bueti/ioverlander_backup:2023-02-05_15-59-41) from registry...
INFO    2023/02/05 17:14:28 Extracting backup from Docker image...
INFO    2023/02/05 17:14:43 Creating database...
INFO    2023/02/05 17:14:44 Database already exists, skipping creation...
INFO    2023/02/05 17:14:53 Restoring database...
INFO    2023/02/05 17:16:41 Some errors during restore where ignored.
Database successfully restored.
{{< /codeWide >}}
