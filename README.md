# Ansible role `Siege`
Installs the loadtesting tool siege 3.1.0 on centos7 as a role in an ansible environment.

An Ansible role for installing `Siege` on RHEL/CentOS 7. Specifically, the responsibilities of this role are to:

- Install Siege version 3.1.0
- Set up the host as a server

## What is Siege?
Siege is a benchmarking and load testing tool that can be used to measure the performance of a web server when under immense pressure. Siege performs following tests:
- Amount of data transferred.
- Response time of server.
- Transaction rate.
- Throughput.
- Concurrency.
- Times the program returned ok.
- 
## Siege provides three modes of operation:

Regression.
Internet Simulation.
Brute Force.

For more information about this loadtesting tools, I recommend to visit the [`Official website`](https://www.joedog.org/siege-home/).

The following things will be done during the installation of this role:
- Update and upgrade your server
- Install Siege version 3.1.0
- install the `Development tools` package group

## Getting started


## Requirements

No specific requirements

## Contributing

Mathias Van Rumst


## License

BSD

## Author Information

Jens De Vreese
