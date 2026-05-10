# Task 1: Understanding Ownership (10 minutes)

* Ran `ls -l` in the home directory
* Identified owner and group columns in Linux file permissions
* Checked which user owns different files
* Understood permission format:

```bash id="q1w2e3"
-rw-r--r-- 1 owner group size date filename
```

* Learned:

  * Owner → user who controls the file
  * Group → shared access for multiple users
  * Others → remaining users in the system

* Practiced reading Linux permission structure and ownership details using:

```bash id="a4s5d6"
ls -l
```

---

# Task 2: Basic chown Operations (20 minutes)

* Created file `devops-file.txt`
* Checked current ownership using:

```bash id="z7x8c9"
ls -l devops-file.txt
```

* Created users if required
* Changed file owner from one user to another
* Practiced ownership modification using:

```bash id="v1b2n3"
sudo chown tokyo devops-file.txt
```

and

```bash id="m4n5b6"
sudo chown berlin devops-file.txt
```

* Verified ownership changes successfully

* Learned:

  * `chown` changes file owner
  * Ownership can be transferred between users

---

# Task 3: Basic chgrp Operations (15 minutes)

* Created file `team-notes.txt`
* Checked current group ownership
* Created new group:

```bash id="k7l8p9"
sudo groupadd heist-team
```

* Changed file group ownership using:

```bash id="h1j2k3"
sudo chgrp heist-team team-notes.txt
```

* Verified updated group ownership using `ls -l`

* Learned:

  * `chgrp` changes only group ownership
  * Groups help manage shared access permissions

---

# Task 4: Combined Owner & Group Change (15 minutes)

* Created file `project-config.yaml`
* Changed both owner and group in one command:

```bash id="p4o5i6"
sudo chown professor:heist-team project-config.yaml
```

* Created directory `app-logs/`
* Updated directory ownership and group:

```bash id="u7y8t9"
sudo chown berlin:heist-team app-logs/
```

* Learned:

  * `chown owner:group` modifies both owner and group together
  * Ownership changes apply to files and directories

---

# Task 5: Recursive Ownership (20 minutes)

* Created project directory structure:

```bash id="r1e2w3"
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

* Created group:

```bash id="q4t5y6"
sudo groupadd planners
```

* Changed ownership recursively:

```bash id="a7s8d9"
sudo chown -R professor:planners heist-project/
```

* Verified recursive ownership changes using:

```bash id="f1g2h3"
ls -lR heist-project/
```

* Learned:

  * `-R` applies ownership changes recursively
  * Parent folder and all contents inherit updated ownership

* Understood difference between:

  * `folder`
  * `folder/*`

---

# Task 6: Practice Challenge (20 minutes)

* Created users:

  * `tokyo`
  * `berlin`
  * `nairobi`

* Created groups:

  * `vault-team`
  * `tech-team`

* Created directory:

```bash id="j4k5l6"
mkdir bank-heist
```

* Created files:

```bash id="z1x2c3"
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

* Assigned different ownerships and groups:

```bash id="v4b5n6"
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

```bash id="m7n8b9"
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

```bash id="q1w2e4"
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

* Verified ownerships using:

```bash id="r5t6y7"
ls -l bank-heist/
```

* Learned:

  * Real-world file access management
  * Multi-user and multi-group ownership handling
  * Linux permission and ownership administration in practical scenarios
