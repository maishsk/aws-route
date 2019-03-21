# aws-subnet

Will create Route tables in an existing VPC    
Private subnets (that have the word Private in their Name tag) will be routed out through its respective NAT 
Gateway in its availability Zone.   
Public subnets (that have the word Public in their Name tag) will be routed out through the Internet Gateway   

## Requirements

- AWS credentials and the correct permissions to create the resources
- An existing VPC with a tagged Name
- Internet Gateway defined and attached to the VPC
- A NAT Gateway defined in each availability Zone

## Role Variables

The variables uses in this role are

| Variable Name | Required | Description | 
|----|----|----|
| `region`| **Yes** | The region that you will deploy into |
| `vpc_name` | **Yes** | Used for identification of VPC |
| `route_purge_routes` | Optional | Purge existing routes that are not found in routes <br> - Default `yes` |
| `route_purge_subnets` | Optional | Purge existing subnets that are not found in subnets <br> - Default `true` |
| `route_purge_tags` | Optional | Purge existing tags that are not found in route table <br> - Default `yes` |

## Dependencies

None

## Example Playbook

### Download dependencies

#### Create requirements file

Create a `requirements.yml` file with the following contents

```
- src: https://github.com/maishsk/aws-route
  version: master
```

#### Download dependencies
Run the following command:
```
ansible-galaxy install -r requirements.yml --force -p .
```

### Create playbook 
Create a `main.yaml` file with the following contents:
```
---
- name: Create Routes
  hosts: localhost
  connection: local
  gather_facts: false
  vars_files:
    - vars/vars.yml
  roles:
    - aws-route
```

Create a `vars/vars.yml` with the content similar to:

```
vpc_name: maish_test
region: us-east-2
```

## Running the playbook

To create the Routes

`ansible-playbook main.yml -e "create=true"`

To remove the Routes

`ansible-playbook main.yml -e "rollback=true"`

## License

BSD

## Author Information
This role was created by [Maish Saidel-Keesing](https://www.maishsk.com/), author of [The Cloud Walkabout](http://cloudwalkabout.com/).