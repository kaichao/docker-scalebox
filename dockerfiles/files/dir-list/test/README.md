# examples for dir-list

## 1. local path

- format
```
    PREFIX_URL=/<local-base-dir>
    message: ${dir}
```

```sh
PREFIX_URL=/ DIR_NAME=etc/postfix REGEX_FILTER=^.*cf\$ scalebox app create

PREFIX_URL=/etc DIR_NAME=postfix REGEX_FILTER=^.*cf\$ scalebox app create

PREFIX_URL=/etc/postfix DIR_NAME=. REGEX_FILTER=^.*cf\$ scalebox app create

```

- dir-entry

```sh
PREFIX_URL=/ DIR_NAME=etc/NetworkManager ENTRY_TYPE=DIR REGEX_FILTER= scalebox app create

PREFIX_URL=/ DIR_NAME=etc/NetworkManager ENTRY_TYPE=DIR REGEX_FILTER='^.+\.d' scalebox app create
```

## 2. rsync-over-ssh

- format
```
    PREFIX_URL=[<ssh-user>@]<ssh-host>:<ssh-port><ssh-base-dir>
    message: ${dir}
```

```sh
PREFIX_URL=scalebox@10.255.128.1/ DIR_NAME=etc/postfix REGEX_FILTER=^.*cf\$ scalebox app create

PREFIX_URL=scalebox@10.255.128.1/etc DIR_NAME=postfix REGEX_FILTER=^.*cf\$ scalebox app create
PREFIX_URL=scalebox@10.255.128.1:22/etc DIR_NAME=postfix REGEX_FILTER=^.*cf\$ scalebox app create

PREFIX_URL=scalebox@10.255.128.1/etc/postfix DIR_NAME=. REGEX_FILTER=^.*cf\$ scalebox app create

```

- dir-entry

```sh
PREFIX_URL=scalebox@10.255.128.1/ DIR_NAME=etc/NetworkManager ENTRY_TYPE=DIR REGEX_FILTER= scalebox app create

PREFIX_URL=scalebox@10.255.128.1/ DIR_NAME=etc/NetworkManager ENTRY_TYPE=DIR REGEX_FILTER='^.+\.d' scalebox app create
```

## 3. rsync-native

- format
```
    PREFIX_URL=rsync://[<rsync-user>[:<rsync-password>]@]<rsync-host>[:<port>]/<rsync-base-dir>
    message: ${dir}
```

- anonymous
```sh
# ncbi data
PREFIX_URL=rsync://ftp.ncbi.nlm.nih.gov/1000genomes/ftp DIR_NAME=. scalebox app create
```

- non-anonymous
```sh
PREFIX_URL=rsync://fast@fast.cstcloud.cn/doi/10.1038/s41586-021-03878-5 DIR_NAME=20191021 scalebox app create
```

## 4. ftp(?)

- format
```
    SOURCE_URL=ftp://[<ftp-user>[:<ftp-pass>]@]<ftp-host>[:<port>]/<ftp-base-dir>
    message: ${SOURCE_URL}~${dir}
```

- anonymous ftp
```sh
PREFIX_URL=ftp://ftp.ncbi.nlm.nih.gov/1000genomes/ftp/release/2008_12 DIR_NAME=. scalebox app create
DIR_NAME=ftp://ftp.ncbi.nlm.nih.gov/1000genomes/ftp/release/2008_12~. REGEX_FILTER=^.*gz\$ scalebox app create

DIR_NAME=ftp://ftp.ncbi.nlm.nih.gov/1000genomes/ftp/release~2008_12 scalebox app create

DIR_NAME=ftp://ftp.ncbi.nlm.nih.gov/~1000genomes/ftp/release/2008_12 scalebox app create

```

- non-anonymous ftp
```sh
PREFIX_URL=ftp://<ftp-user>:<ftp-pass>@<ftp-host>/<ftp-path> DIR_NAME=. scalebox app create
```

## 5. 2D-dataset(removed)
```sh
DIR_NAME=/raidz/fast-fz/ZD2022_1_1~Dec+4120_03_03/20221102 \
REGEX_2D_DATASET='^(.+%)?([^/]+/[^/]+)/.+M([0-9]+)_([0-9]+).+$' \
INDEX_2D_DATASET='2,3,4' \
scalebox app create

```
