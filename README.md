# Client for file-transfer
## Components:

- Indexer
- Watcher
- Internal DB
- Chunker

`Client` app monitors the folders that are identified as workspace or sync folders and synchronized them with the remote `Cloud Storage`. Client upload and download files, detecting file changes in the sync folder and handling conflicts while updates file.

The `client` interacts with the `Synchronization Service` to handle file metadata updates (e.g. file name, size, modification date, etc.)

The `client` interacts with the backend `Cloud Storage`  for storing the actual files.


## Chunker. 
Break the files in to multiple chunks and reconstructing a file from these chunks. This algorithm should detect the parts of the files that have been modified by user and the transfer those parts to the `Cloud Storage`.

## Indexer.
Receive events from the `Watcher` and updates the `Internal DB` with info about the chunks of the modified files. Once the chunks are successfully submitted to the `Cloud Storage`, the `Indexer` will communicate with `Synchronization Service` using the `Message Queuing Service` to update the `Metadata Database` with changes.

## Watcher.
`Watcher` monitors the sync folders and notifies the `Indexer` of any action performed by the user for example when user create, delete, or update files or folders.

## Internal DB.
Store local copy of all the files and chunks information, their versions and their location in the file system.

