Azure CLI for VMSS – Getting started

Installing Azure CLI from Internal branch

1)	Goto https://github.com/AzureRT/azure-xplat-cli/releases 

2)	Run the command npm install –g https://github.com/AzureRT/azure-xplat-cli/archive/vmss.tar.gz using CMD prompt. Below is a list of issues you might face on Windows
    a.	If the command does not run, you will need to run it without the –g 
    b.	Node.js not installed error. You will need to install Node.js and ensure that the PATH system variable is updated to point to the Node folder
    c.	Python is not installed error. You will need to install Node.js and ensure that the PATH system variable is updated to point to the Python folder
    d.	.NET SDK not installed. You will need to install .NET SDK (You might choose to install Visual Studio itself)
    e.	After all this, you might see an error that CL.exe is missing. This is the C++ compiler that you will need to install. (I had visual studio installed and I created a C++ hello world application and ran it. At this point the IDE prompted that I should probably install the compiler and directed me to so)
    f.	Please restart your system

3)	At this point your installation should be complete without any errors. [Please report any issues if that is not the case]

4)	Now if you type the command >Azure, you will not see the VMSS command in the help. That is because you did not install it globally (remember removing the –g)
5)	 You need to navigate to your C:\...\cli\node_modules\azure-cli on CMD prompt and type 
?	Node bin\azure -> now you should see VMSS and VMSSVM .
?	Now you can run all commands but need to use > node bin\azure vmss quick-create… to ensure that you point to the local folder where VMSS module is loaded.
