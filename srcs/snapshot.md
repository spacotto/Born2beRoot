# About Snapshots
A Virtual Machine (VM) snapshot captures the state and data of a VM at a specific point in time, including its configuration, disk data, and optionally its memory and hardware settings. It functions as a restore point, allowing administrators to revert the VM to a previous state quickly, which is particularly useful for testing, configuration changes, or software updates. 

>[!WARNING]
>However, snapshots are not a replacement for comprehensive backup solutions because they are dependent on the original disk, can grow large over time, and cannot be used to recover individual files or restore to a different VM.

## How to generate a snapshot on VirtualBox
Snapshots are created by the **hypervisor** (such as VMware, Hyper-V, or Proxmox) and typically use a copy-on-write (COW) mechanism, where subsequent changes are stored in delta files, minimizing initial storage overhead.

>[!WARNING]
>The way you generate (and, thus, remove snapshots) depends on the tool you're using.

To generate a Virtual Machine (VM) snapshot in VirtualBox, do as follows.

**STEP 1**
>First, ensure the **VM is powered off** or running, as snapshots can be created while the VM is running, though it will be paused during the process.
   
**STEP 2**
>Launch the VirtualBox application and **select the VM** for which you want to create a snapshot.
   
**STEP 3**
>Navigate to the "**Snapshots**" section by clicking on the **hamburger menu** (three horizontal lines) to the right of the VM name and **selecting "Snapshots"**.[
>[!NOTE]
>If this is your first snapshot, the list will only show "Current State."

**STEP 4**
>Click the "**Take**" button located at the top-left of the Snapshots window.
>[!NOTE]
>In the dialog that appears, provide a descriptive name for the snapshot, such as "Fresh installation" or "After software update," to help identify its purpose later.
>[!TIP]
>Optionally, add a **description** to note the state of the VM at that point, such as specific configurations or software installed (just like when you `git commit -m "Description"`). You can also choose whether to include the **current memory state** in the snapshot; checking this option saves the VM's running state, which can be u**seful for quick restoration but increases the snapshot size**.

**STEP 5**
>After setting the **name** and **options**, click "**OK**." The snapshot creation process **may take a few moments**, depending on the VM's size and activity. Once complete, the **new snapshot will appear in the list**, and the current state of the VM will be based on this snapshot.

>[!NOTE]
Snapshots are stored as **differencing disk files** in a "Snapshots" folder within the VM's directory, which only store changes from the previous state, helping to conserve disk space. You can create multiple snapshots to maintain different points in time, and later restore to any of them by selecting the desired snapshot and clicking "Restore".

>[!WARNING]
>Note that restoring a snapshot requires the VM to be powered off.

## How to remove a snapshot on VirtualBox
To remove a virtual machine snapshot in Oracle VM VirtualBox, you can use either the **graphical user interface (GUI)** or the **command-line interface (CLI)**. 

### Graphical User Interface (GUI)
1. Select the virtual machine in the main window.
2. Click the "Snapshots" button in the upper-right corner.
3. Right-click the snapshot you wish to delete in the snapshots tree.
4. Select "Delete" from the context menu.

>[!NOTE]
>This action releases the disk space used by the snapshot's data but does not affect the current state of the VM.

>[!WARNING]
>The deletion process **may take considerable time**, especially for large snapshots, as data is merged between disk image files, and temporary files may require additional disk space during the operation.

### VBoxManage command-line tool
Alternatively, use the VBoxManage command-line tool:
1. List the snapshots with VBoxManage snapshot "VM_NAME" list to identify the snapshot name or UUID,
2. Execute VBoxManage snapshot "VM_NAME" delete "SNAPSHOT_NAME" to delete the specified snapshot.
>[!NOTE]
>This command can be used even while the VM is running, though some operations may require the VM to be shut down.

>[!TIP]
>For deleting multiple snapshots, a script can automate the process by reading snapshot names from a text file and executing the delete command for each one.
