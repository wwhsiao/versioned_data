## Galaxy "Versioned Data" Library Setup

1. Create a Galaxy data library called "Versioned Data".  The name is important - it must be located by the Versioned Data tool.

![Galaxy Data Library](galaxy_data_library.png)

2. Set permissions so the special "versioneddata@localhost.com" user has add/update permissions on the "Versioned Data" library.

3. Then add any folder structure you want under Versioned Data.  Top level folders could be "Bacteria, Virus, Eukaryote", or "NCBI, ... ".  Underlying folders can hold versioned data for particular bacteria / virus databases, e.g. "NCBI nt".

4. Connect a **"pointer.[data store type]"** file (a simple text file) to any folder that you want to activate as a versioned data store.  Any folder that has a "pointer.[data store type]" file in it will be treated as a folder containing versioned content, as illustrated above.  These folders (their names) will then be included in the Versioned Data tool's list of data stores. Within these folders, links to caches of retrieved versioned data will be kept (shown as "cached data" items in illustration).  For "folder" and "biomaj" data stores, links will be to permanent files, not cached ones.

For example, on Galaxy page Shared Data > Data Libraries > Versioned Data, there is a folder/file:

  `Bacterial/RDP RNA/pointer.kipper`

which contains one line of text:

  `/projects2/ref_databases/versioned/rdp_rna/`

That enables the Versioned Data tool to list the Kipper archive as "RDP RNA" (name of folder that pointer file is in), and to know where its data store is. Beneath this folder other cached folders will accumulate.

The "upload files to a data library" page (shown below) has the ability to link to the pointer file directly in the data store folder.  Select the displayed "Upload files from filesystem paths" option (available only if you access this form from the admin menu in Galaxy).  Enter the path and FILENAME (literally "pointer.kipper" in this case) of your pointer file. If you forget the filename, galaxy will link all the content files, which will need to be deleted before continuing.

![Link pointer file to Versioned Data subfolder](library_dataset_upload.png)

Preferably select the "Link to files without copying into Galaxy" option as well.  This isn't required, but linking to the pointer file enables easier diagnosis of folder path problems.

Then submit the form; if an error occurs then verify that the pointer file path is correct.

**Note: a folder called "Workflow Cache" is automatically created within the Versioned Data folder to hold cached workflow results as triggered by the Versioned Data tool. No maintenance of this folder is needed.**

### Direct use of Data Library Folder

Note: The "folder" data store is a simple data store type - marking a folder this way enables the Versioned Data tool to directly list the subfolders of this Library folder (by name), with expectation that each folder's contents can be placed in user's history directly.  The one optional twist to this is that if the folder's .pointer file is sym-linked to another folder on the server, then folder contents will be retrieved from the symlinked location. 

