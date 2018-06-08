# RememberThisCommand

Simple CLI utility to keep track of hard-to-rember commands instead of fishing
them out of a Bash history.

Each command record consists of a tag, which allows command grouping, a command, and an optional note, which describes what the command does.

## Usage
* Adding a command
```
$ rtcmd --tag git --command "git commit -m 'commit message'" --note "Commit without an editor"
```

* Listing saved commands
```
$ ./rtcmd --list

--- bugzilla ---
    3 | bugzilla query --component <component> --outputformat "%{id}" --status NEW,ASSIGNED,POST,MODIFIED,ON_DEV,ON_QA,VERIFIED
      | Get IDs of opened bugs for given components

--- git ---
    1 | git commit -m 'commit message'
      | Commit without an editor
    2 | log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
      | Fancy git log

$ ./rtcmd --list bugzilla

--- bugzilla ---
    3 | bugzilla query --component <component> --outputformat "%{id}" --status NEW,ASSIGNED,POST,MODIFIED,ON_DEV,ON_QA,VERIFIED
      | Get IDs of opened bugs for given components
```

* Deleting a command
```
$ ./rtcmd --delete 2
$ ./rtcmd --list

--- bugzilla ---
    3 | bugzilla query --component <component> --outputformat "%{id}" --status NEW,ASSIGNED,POST,MODIFIED,ON_DEV,ON_QA,VERIFIED
      | Get IDs of opened bugs for given components

--- git ---
    1 | git commit -m 'commit message'
      | Commit without an editor
```

* Searching in saved commands
```
$ ./rtcmd --search "%bugs%"

--- bugzilla ---
    3 | bugzilla query --component <component> --outputformat "%{id}" --status NEW,ASSIGNED,POST,MODIFIED,ON_DEV,ON_QA,VERIFIED
      | Get IDs of opened bugs for given components
```
Note: the search term is in an SQL syntax - % matches zero or more characters, ? matches zero or one character.
