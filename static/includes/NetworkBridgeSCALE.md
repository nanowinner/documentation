&NewLine;

To set up a bridge interface, from the **Network** screen:

1. Click **Add** in the **Interfaces** widget.
The **Add Interface** configuration screen displays.

{{< trueimage src="/images/SCALE/Network/AddInterfaceNicDeviceSCALE.png" alt="Add Bridge Interface" id="Add Bridge Interface" >}}

2. Select **Bridge** from the **Type** dropdown list.
You cannot change the **Type** field value after you click **Save**.

3. Enter a name for the interface.
Use the format *bondX*, *vlanX*, or *brX* where *X* is a number representing a non-parent interface.
Read-only when editing an interface.
You cannot change the **Name** of the interface after you click **Save**.

4. (Optional but recommended) Enter any notes or reminders about this particular bridge in the **Description** field.

5. Select the interfaces on the **Bridge Members** dropdown list.

6. Next to **Aliases** click **Add** to enter the IP address for this bridge interface.
(Optional) click **Add** to display an additional IP address field for each additional IP address you want to add.

{{< trueimage src="/images/SCALE/Network/AddInterfaceNicDeviceOtherSettingsSCALE.png" alt="Add IP and Subnet Mask" id="Add IP and Subnet Mask" >}}

7. Click **Save** when finished.
The created bridge shows in **Interfaces** with its associated IP address information.

{{< trueimage src="/images/SCALE/Network/NetworkInterfacesBridgeSCALE.png" alt="Network Interfaces with Bridge" id="Network Interfaces with Bridge" >}}

8. To determine if network changes are successful, click **Test Changes**.

{{< trueimage src="/images/SCALE/Virtualization/VMTestNetworkChanges.png" alt="Test Network Changes" id="Test Network Changes" >}}

9. Once TrueNAS finishes testing the interface, click **Save Changes** if you want to keep the changes. Click **Revert Changes** to discard the changes and return to the previous configuration.

{{< trueimage src="/images/SCALE/Virtualization/VMSaveNetworkChanges.png" alt="Save Network Changes" id="Save Network Changes" >}}

{{< expand "Troubleshooting Network Changes" "v" >}}
Occasionally, a misconfigured bridge or a conflict with a running application, VM, or service can cause the network changes test to fail.
Typically, this is because the bridge is configured using an IP address that is already in use.
If the system does not receive a **Save Changes** check-in before the test times out (default 60 seconds), TrueNAS automatically reverts all unsaved changes.

The following troubleshooting options are available if you are unable to save the new bridge and network changes.
Options are ordered from the least to the most disruptive.
Try options one and two before proceeding with option three and then four.

  1. Ensure that there are no currently running applications.
  2. Stop any running VMs.
  3. (Optional) Go to **Services**.
  Click <span class="material-icons">edit</span> **Configure** to view the current configuration of sharing services including **SMB** and **NFS**.
  Stop any services that have a bind IP address matching the bridge IP address.
  Restart the service(s) after network changes are tested and saved.
  4. (Optional) Stop the Kubernetes service.
  Connect to a shell session and enter `systemctl k3s.service stop`.
  Press <kbd>Enter</kbd>.
  After network changes are tested and saved, restart Kubernetes with `systemctl k3s.service start`.

{{< /expand >}}
