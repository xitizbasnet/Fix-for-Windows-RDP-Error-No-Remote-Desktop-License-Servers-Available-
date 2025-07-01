### ✅ **Fix for Windows RDP Error: "No Remote Desktop License Servers Available"**

---

#### **Summary**

When attempting to log into a virtual machine (VM) via Remote Desktop Protocol (RDP), users may encounter the following error:

> **"The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license. Please contact the server administrator."**

This issue typically arises due to the expiration of the RDP licensing grace period on the Windows Server. The fix involves a registry modification to reset the grace period.

---

### 🛠️ **Resolution Steps**

#### **Step 1: Attempt RDP Login**

* Try logging into the VM via RDP:

  * ✅ If login is successful, no action is required.
  * ❌ If login fails with the license server error, proceed to Step 2.

---

#### **Step 2: Access VM via VMware ESXi Console**

* Use the **VMware ESXi interface** to access the affected VM directly.

---

#### **Step 3: Modify the Registry to Reset Grace Period**

1. **Open the Registry Editor**

   * Press `Win + R`, type `regedit`, and press Enter.

2. **Navigate to the Following Registry Path:**

   ```
   Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\RCM\GracePeriod
   ```

   **Step-by-step navigation:**

   * `Computer`

     * `HKEY_LOCAL_MACHINE`

       * `SYSTEM`

         * `CurrentControlSet`

           * `Control`

             * `Terminal Server`

               * `RCM`

                 * `GracePeriod`

3. **Set Permissions on the GracePeriod Key:**

   * Right-click on the `GracePeriod` key and select **Permissions**.
   * Select **Administrators** from the list.
   * Check **Allow** for the following:

     * ✅ Full Control
     * ✅ Read
     * ✅ Special Permissions (if available)
   * Click **OK** to apply.

4. **(Optional)**:

   * Delete the **binary value** under `GracePeriod` **only if instructed by IT policy**.

5. **Reboot the Server:**

   * After applying the changes, **reboot the VM**.

---

### ✅ **Result**

Upon successful reboot, RDP access should be restored without the license server error.

---

### ⚠️ **Notes**

* This procedure is intended for **temporary relief**.
* A **permanent solution** requires installing and activating a **Remote Desktop Licensing Server**.
* Always **back up the registry** before making changes.
* Ensure compliance with **Microsoft licensing policies**.

---

### 📜 **Revision History**

| Version | Date       | Author        | Description                  |
| ------- | ---------- | ------------- | ---------------------------- |
| 1.0     | 2025-07-01 | IT Department | Initial creation of document |

---
