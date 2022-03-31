# schematics-chaos-test
Perform resiliency test of the reference application using the ansible-controlled-failure-injectors library

Use this repo to test the failure inject scenarios present in repo [ansible-controlled-failure-injectors](https://github.ibm.com/schematics-solution/ansible-controlled-failure-injectors) using the playbooks.

### Suppprted testing scenarios

* Making cluster pod down (kill a specific pod by providing cluster id, pod name and namespace it belongs to as an inputs.)

## How to Execute Playbook

* Login to ibmcloud using api key

   ```
   ibmcloud login --apikey <your ibmcloud api key>
   ```

* Run following command to generate authentication tokens

  ```
  ibmcloud iam oauth-tokens
  ```

* Export IAMRefreshToken and IAMToken values from ~/.bluemix/config.json file

  ```
  E.g:

  export IC_IAM_TOKEN=eyJraWQiOiIyMDIyMDMxNzA4MjMiLCJhbGciOiJSUzI1NiJ9.eyJpYW1faWQiOiJJQk1pZC01NTAwMDQ4WVFYIiwiaWQiOiJJQk1pZC01NTAwMDQ4WVFYIiwicmVhbG1pZCI6IklCTWlkIiwic2Vzc2lvbl9pZCI6IkMtOD

  export IC_IAM_REFRESH_TOKEN=eyJhbGciOiJydCJ9.eyJzZXNzaW9uX2lkIjoiQy04MmJmNGZhMy0yMmY0LTQwYTAtYmQwMS0zYmVmZWE4MGZhNDkiLCJpYW1faWQiOiJJQk1pZC01NTAwMDQ4WVFYIiwiYWNjb3
  ```

* As a final step, run following command to execute playbook
 
  ```
  ansible-playbook ./playbook/pod_failure.yml --extra-vars "cluster_id=<your_cluster_id>" -vvv
  ```

## Schematics Chaos Test Directory Structure

| Subdirectory             | Description                                           | 
|--------------------------|-------------------------------------------------------|
| group_vars | Directory is used to capture variables for host groups. Each host group should have its own file under this directory |
| host_vars | Directory is used to capture variables for individual hosts. Each host should have its own file under this directory.|
| playbooks | List of playbooks.|
| ansible.cfg | Certain settings in Ansible are adjustable via a configuration file.|
| hosts     | An inventory defines a collection of hosts that Ansible will manage.|


### NOTE:

In inventory file, two host groups always exist:
• The all host group contains every host explicitly listed in the inventory.
• The ungrouped host group contains every host explicitly listed in the inventory that is not a member of any other 
  group.

## How to add git submodule (Adding ansible-controlled-failure-injector as a submodule)

A sub-module is a repository embedded inside another repository. The sub-module has its own history; the repository it is embedded in is called a super-project

Run following command to add submdule
```
git submodule add -b master git@github.ibm.com:schematics-solution/ansible-controlled-failure-injectors.git
```

To update the already existing sub-module, run

```
# Change to the submodule directory
cd ansible-controlled-failure-injectors

# Checkout desired branch
git checkout master

# Update
git pull

# Get back to your project root
cd ..

# Now the submodules are in the state you want, so
git commit -am "Pulled down update to ansible-controlled-failure-injectors"
```


