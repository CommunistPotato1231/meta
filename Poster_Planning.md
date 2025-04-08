# Agenda

## Background

### z/OS Background
- Operating system for IBM mainframe systems
- Extremely reliable and scalable system handling large user bases with 99.999% uptime
- Very secure operating system – used by banks and governments for financial transactions

### Zopen Community Background
- Aimed at improving the developer experience and bridging the technology gap between z/OS and other mainstream operating systems

## Motivation
- Having few open-source tools in z/OS makes it much more difficult to develop programs on the IBM mainframes
- Goal: Make the lives of IBM developers easier and make it more approachable to begin developing z/OS applications

## Objectives

### Porting a Tool to z/OS

#### Redis Background
- Redis is often referred to as a data structures server
- Provides access to mutable data structures via a set of commands using a server-client model with TCP sockets
- Allows different processes to query and modify shared data structures

#### Key Properties of Redis
- Stores data on disk while serving and modifying it in memory
- Emphasizes memory efficiency; Redis structures use less memory than high-level language equivalents
- Offers database-like features: replication, tunable durability, clustering, and high availability

#### Example Usage
> _(Maybe add a simple example of how to use Redis here)_

## What’s Remaining

### Enhancing the Zopen Package Manager

#### Background on the Zopen Package Manager
- Custom package manager created for z/OS
- Executes multiple commands for information on packages and their dependencies
- Downloads and builds open-source tools locally

#### Desired Features
- `zopen-diagnostics`: Prints out important information about your code environment, useful for bug reporting
  - Outputs system information like architecture, z/OS version, disk space, and root directory info
- `zopen-info`: Enhanced to fix issues with tagged versions
  - Added logic to check for a tag and retrieve the tagged version if it exists

## Challenges
- Understanding how z/OS works
- Learning the structure and build process of open source projects
- Working with a CLI interface
- Debugging projects with hundreds of source files
- Learning regex expressions and bash scripting
- Using Git CLI effectively

## Results
- ✅ Successfully ported Redis  
  - [Redis Port GitHub Repo](https://github.com/zopencommunity/redisport.git)
- ✅ Created pull request
- ✅ Successfully implemented `zopen-diagnostics` and `zopen-info` enhancements
- ✅ Updated documentation

## References
- [https://zopen.community](https://zopen.community)
- [https://github.com/zopencommunity](https://github.com/zopencommunity)
- [Redis Port GitHub Repo](https://github.com/zopencommunity/redisport.git)
- _(List of your PRs and commits can go here)_

## Where It Needs Help
_(Describe areas where assistance or future development is needed)_
