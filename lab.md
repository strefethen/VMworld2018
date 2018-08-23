# VMworld 2018 Python SDK Hackathon

## Install Python
Go to: [downloads](https://www.python.org/downloads/) and download and install Python for your Platform.
The SDK supports both python2 and python3, but we recommend to install the latest version of python3. 

## Setup Python SDK

Create and activate a virtual env:

#### Python2: 

    virtualenv <env_dir>

#### Python3:

| Windows | OSX |
|---------|-----|
|```py -m venv <env_dir>```|```python3 -m venv <env_dir>```|

#### Activate your virtual env:

| Windows | OSX |
|---------|-----|
|```<env_dir>\Scripts\activate```|```source <env_dir>/bin/activate```|

##  Clone the github repo
The python github repo is located [here](https://github.com/vmware/vsphere-automation-sdk-python)

```bash
git clone https://github.com/vmware/vsphere-automation-sdk-python
```
Or optionally [download](https://github.com/vmware/vsphere-automation-sdk-python/archive/master.zip) the SDK from Github as a .zip file and unzip it to the current dir.

##  Install dependencies

```bash
cd <sdk-dir>
pip install -r requirements.txt --extra-index-url <file:///abs_path/to/sdk/lib/>
```

## vSphere Python SDK Examples
Start the Python command interpreter:

#### Linux/Mac:

    python3

#### Windows:

    py

## List VC inventory in interactive mode

### Connect to the vSphere REST API endpoint

```python
Python 3.6.5 (default, Apr 25 2018, 14:26:36)
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from vmware.vapi.vsphere.client import create_vsphere_client
```

Connect to a vCenter Server using username and password

```python
>>> vsphere_client = create_vsphere_client(server='vcenter.sddc-34-218-2-64.vmwarevmc.com', username='cloudadmin@vmc.local', password='hoEx84v%#r')
```

### Make API calls using the Python Interpreter

Example API calls
```python
>>> vsphere_client.vcenter.VM.list()
...
>>> vsphere_client.vcenter.Datacenter.list()
...
>>> vsphere_client.vcenter.Cluster.list()
...
>>> vsphere_client.vcenter.Host.list()
...
>>> vsphere_client.vcenter.Folder.list()
...
>>> vsphere_client.vcenter.Datastore.list()
```

### Find a specific host using a filter spec

```python
>>> filter_spec = Host.FilterSpec(names=set([“<HOST_IP_Address>“]))
vsphere_client.vcenter.Host.list(filter_spec)
```

### Find a VM in Folder1
```python
>>> from com.vmware.vcenter_client import VM, Folder

>>> folder_filter = Folder.FilterSpec(names=set([‘Folder1’]))
>>> folder_id = client.vcenter.Folder.list(folder_filter)[0].folder

>>> vm_filter = VM.FilterSpec(folders=set([folder_id]))
>>> client.vcenter.VM.list(vm_filter)
```

Note: To exit interactive Python simply type quit() and press Return:

```python
quit()
```

## Run SDK samples

### Set PYTHONPATH to use SDK helper methods  

#### Linux/Mac:

    export PYTHONPATH=${PWD}:$PYTHONPATH

#### Windows:

    set PYTHONPATH=%cd%;%PYTHONPATH%

## To get help running the SDK samples

Use -h command line option, for example:

```python
python samples/vsphere/vcenter/vm/list_vms.py -h
```

### Run VMC Deploy OVF Sample (VMC)

The following sample will create a VM from an OVF template and upon completion cleanup and delete the VM:

```bash
$ python samples/vmc/sddc/deploy_ovf_template.py -s 'vcenter.sddc-34-218-2-64.vmwarevmc.com' -u 'cloudadmin@vmc.local' -p 'hoEx84v%#r' -v --lib 'basic.ovf'

vcenter server = vcenter.sddc-34-218-2-64.vmwarevmc.com
vc username = cloudadmin@vmc.local
Resource pool ID: resgroup-61
Library item ID: d89d381d-2a83-47c2-bc63-09ce98295897
Found an OVF template: vmBV8ly to deploy.
Deployment successful. Result resource: VirtualMachine, ID: vm-90
```

### Verify the new VM is deployed successfully

Run the list VMs sample

```bash
python samples/vsphere/vcenter/vm/list_vms.py -s 'vcenter.sddc-34-218-2-64.vmwarevmc.com' -u 'cloudadmin@vmc.local' -p 'hoEx84v%#r'
```

### VM Power Commands Sample

```bash
python samples/vsphere/vcenter/vm/power.py -s 'vcenter.sddc-34-218-2-64.vmwarevmc.com' -u 'cloudadmin@vmc.local' -p 'hoEx84v%#r' -n 'VM3'
```

## Exercises
Try to use the sample_template to create three scripts and then run them:

* Power on/off the VM you created
* Edit VM cpu/memory
* Add a CD-ROM to your VM
