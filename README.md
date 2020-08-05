# get_deploy_host

This is a Python command line utility that maintains a JSON list of host
names and deployed branches. You can use this inside an Ansible playbook 
to determine a host name when deploying a test branch.

Usage:
```
get_deploy_host [-h] [--user USER] [--inputfile INPUTFILE]
				   [--repository REPOSITORY]
				   branch_name
```

`branch_name` is the only required parameter.


## Background
We have a pool of N testing hosts where we can deploy our web applications
for acceptance testing. When deploying a new branch, we want to re-use the
least-recent used host name. 

After you do a deployment, commit the changes `deployments.json` to the
repository, so other people deploying have the most recent version of the
deployment status. The Ansible playbook might do this automatically.

## Storage file `deployments.json`

The file contains an array of deployment objects. Each object must have at
least a `host` key. The script orders the deployments by descending deploy
date (in the key `deployedOn`).
