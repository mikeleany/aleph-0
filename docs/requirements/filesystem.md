# Filesystem

Describes the filesystem(s) supported by Aleph-0 and the operations available to
users and programs.

## Overview

Aleph-0 supports a single ext2 filesystem, mounted as the root filesystem at boot. The
filesystem resides on a block storage device separate from the boot ISO. Aleph-0 does
not format filesystems; the ext2 volume must be pre-formatted before use.

## ext2 Support

Aleph-0 supports a subset of the ext2 filesystem specification.

### Supported Operations

- Creating, reading, writing, and deleting files
- Creating and deleting directories
- Listing directory contents
- Renaming and moving files and directories
- Hard links

### Unsupported Features

The following ext2 features are not supported:

- Symbolic links
- Extended attributes
- Access control lists (ACLs)
- Multiple users and groups

### Feature Flags

At mount time, Aleph-0 checks the filesystem's feature flags:

- Filesystems with unsupported incompatible features are rejected and will not be
  mounted
- Filesystems with unsupported read-only compatible features are rejected and will not
  be mounted
- Unsupported compatible features are ignored

## Permissions

Aleph-0 operates as a single user. File permission checks use only the owner permission
bits (read, write, and execute) from the inode. Group and other permission bits are
ignored.

## Size Limits

No size limits are imposed beyond those inherent to the ext2 specification.
