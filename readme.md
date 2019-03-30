# Task #3: Building a Dynamic CI Infrastructure ##


## CI servers table ##

  | IP ADDR      | HOST NAME         | COMPONENTS to INSTALL | PORTS EXPOSED TO HOST (vm port->host) |
  | -------------| ---------------   | ----- | ----- |
  | 172.16.1.101 | artifactory.cilab | `nexus`, `java` | 8081->38081 |
  | 172.16.1.102 | gitserver.cilab | `gitlabserver` | 80->38000 |
  | 172.16.1.103 | buildserver.cilab| `jenkins`, `SCM tools`, `BUILD tools` | 8080->38080 |
  | 172.16.1.104 | buildnode.cilab | `SCM tools`, `BUILD tools` | 80->38095 |

## Artifact structure
````bash
ci-environment
├── Documentation
│   ├── diagram.png
│   └── diagram.xml
├── config
│   └── hosts
├── machines-user-data
│   ├── artifactory.sh
│   ├── buildnode.sh
│   ├── buildserver.sh
│   ├── common.sh
│   └── gitserver.sh
├── readme.md
└── vagrantfile
````


## The Configuration File
Here i'm going to demonstrates how to do this, using a **hosts** file

First we create hosts configuration file, and put it in a **config/** directory:
```bash
cat > ./config/hosts <<'EOF'
172.16.1.101 artifactory.cilab
172.16.1.102 gitserver.cilab
172.16.1.103 buildserver.cilab
172.16.1.104 buildnode.cilab
EOF
```


## The Vagrantfile
As the Vagrant’s configuration ,`Vagrantfile`, is a ruby script we can build our ci environment.
We read in the configuration file, and then use this to dynamically spin up the systems.

This script has the following feartures
- Configure each system with a hostname specified in the `config/hosts` configuration file
- Configure an NIC with a IP addressed specified in the `config/hosts` file. This allows the virtual guest systems to talk to each other, as well as access them from the host system
- Configure port forwarding to allow you to access a ports on host machine and have all data forwarded to a virtual guest ports
- Provisioning shell scripts based on **hostname** for each system in located in the `machine-user-data/`

## Access - CI Servers
We spoke earier about hosts exposed ports on each system.  
We can open our host browser and browse into desired system.

For Example: gitlab guest machine running on ``port 80`` and we exposed ``port 38000``on our host machine

In order to access to gitlab ,simply  browse to ``http://localhost:38000``
