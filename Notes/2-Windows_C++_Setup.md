# Setting Up C++ Development Environment on Windows

Follow these steps to set up C++ development on Windows using Visual Studio.

### **1. Download and Install Visual Studio Installer**
- Visit [Visual Studio](https://visualstudio.microsoft.com/) and download the installer.
- Launch the installer after the download completes.

### **2. Select Visual Studio Version**
- In the installer, choose the latest version of Visual Studio available.

### **3. Select Workloads**
- Check the following workloads:
  - **Desktop Development with C++**
  - **.NET Desktop Development**

### **4. Install and Launch Visual Studio**
- Click **Install** and wait for the installation to complete.
- Launch Visual Studio after the installation.

### **5. Theme Selection (Optional)**
- Go to **Tools** > **Options** > **Environment** > **General** > **Color Theme** to select your preferred theme.

### **6. Apply Cherno's Settings (Optional)**
If you want to use the same settings as Cherno:
1. Download Cherno's settings from [here](https://thecherno.com/vs).
2. Copy the downloaded file.
3. Paste it in this location: `C:\Users\<your_user_name>\AppData\Local\Microsoft\VisualStudio\17.0_0b79a212\Settings`
4. Open Visual Studio and navigate to:
   - **Tools** > **Import and Export Settings** > **Import Selected Environment Settings**
   - Select **No, just import new settings**
   - Choose **My Settings** and select the Cherno settings file
   - Click **Finish** and close Visual Studio.
   - Reopen Visual Studio to apply the changes.

### **7. Create a New Project**
1. Select **New Project Solution**.
2. In **Solution Explorer**, select **Source Files**.
3. Right-click and choose **Add New Item**.
4. Select **Empty C++ File** and start coding.

