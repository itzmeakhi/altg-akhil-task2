# Get System Specifications Playbook

This Ansible playbook is designed to retrieve system specifications for all linux hosts in your environment. It collects information about CPU, memory, and disk size for each host and saves the output in a structured JSON format.

## Prerequisites
- Ansible installed on the machine running the playbook.
- Appropriate SSH access to all target hosts.
- Privilege escalation privileges for `become: yes`.

## Usage

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/your-repo.git
   
2. **Edit the hosts file:**

   Include the IP addresses or hostnames of your target machines. 

   Note: hosts file is usually present in /etc/ansible/hosts. Refer hosts.sample file here for a reference.

3. **Run the playbook:**
   ```bash
   ansible-playbook get_system_spec.yml -i path/to/your/inventory/hosts


## Playbook Explanation
The playbook consists of the following tasks:

1. **Display CPU Information**
Uses the debug module to display information about the CPU of each host.
Registers the output in the variable cpu_output.
2. **Display Memory Information**
Uses the debug module to display information about the memory of each host.
Registers the output in the variable memory_output.
3. **Display Disk Size Information**
Uses the debug module to display information about the disk size of each host.
Registers the output in the variable disk_output.
4. **Create Output Directory**
Uses the ansible.builtin.file module to create an output directory in /etc/ansible/.
Ensures the directory exists to store output files.
5. **Save Output to a Single File for All Hosts**
Uses the ansible.builtin.copy module to save the gathered information in a structured JSON format.
Iterates through all hosts and compiles the information into a single JSON file located at /etc/ansible/output/out-get_sysspec_all_hosts.json.

## Output Format
The output JSON file will have the following structure:
```json
{
    "host1": {
    "Host": ,
    "CPU Information": [
    "0",
    "GenuineIntel",
    "Intel(R) Xe xxxx"
],
    "Memory Information": {
    "nocache": {
        "free": 849,
        "used": 103
    },
    "real": {
        "free": 277,
        "total": 952,
        "used": 675
    },
    "swap": {
        "cached": 0,
        "free": 0,
        "total": 0,
        "used": 0
    }
},
    "Disk Size Information": [
    {
        "block_available": 1656774,
        "block_size": 4096,
        "block_total": 2094075,
        "block_used": 437301,
        "device": "/dev/xvda1",
        "fstype": "xfs",
        "inode_available": 4145135,
        "inode_total": 4193216,
        "inode_used": 48081,
        "mount": "/",
        "options": "rw,noatime,attr2,inode64,logbufs=8,logbsize=32k,noquota",
        "size_available": 6786146304,
        "size_total": 8577331200,
        "uuid": "2518854e-2cb3-4f56-9f94-04d5d59709de"
    }
]

  },
  }

```

##### -THE END -
