# WindFind
A high performace file locator for instantly finding files and folders by name.

_Hello WindFind :rose:, hello world!_

**If you want a high performance SSH/Telnet/Serial/Shell client, you can try [WindTerm](https://github.com/kingtoolbox/windterm).**

**If you want a high performance text editor, you can try [WindEdit](https://www.github.com/kingToolbox/WindEdit/).**

# Background
When developing [WindTerm](https://github.com/kingToolbox/WindTerm), I need a fast file locator, so WindFind was created as a by-product. Hope it is a good by-product.

# License
**Completely FREE for commercial and non-commercial use without limitations. All released source codes (except thirdparty directory) are provided under the terms of Apache-2.0 license.**

# Download

**Windows binary**: https://github.com/kingToolbox/WindFind/releases

**Linux binary** and **MacOS binary** will be released soon, stay tuned! 

# Source Code

Since WindFind is just a by-product of WindTerm, and all the source code is shared with WindTerm, if you have any source code requirements, please visit [WindTerm](https://github.com/kingtoolbox/windterm).

Please note that **WindTerm**, **WindEdit**, and **WindFind** are all **partial** open source projects.

# Issues and feature requests

Any issues and feature requests are welcome.

Please click [issues](https://github.com/kingToolbox/WindFind/issues) to commit an issue or a feature request.

Please click [Discussion](https://github.com/kingToolbox/WindFind/discussions) to discuss any topics related to file systems, indexing, and performance improvements.

# Screenshots

# Features

- Whether indexing, searching, or outputting, it is incredibly fast.
- Indexing files is highly optimized, generating **only 4 MiB of index data for every million files**.
- Supports indexing files from any file system, similar to `everything`, `locate`, `mlocate`, `plocate`.
- Supports displaying file lists, similar to `dir`, `ls`, but very fast.
- Supports displaying a tree view of file lists, similar to `tree`, but very fast.
- Supports calculating folder sizes, similar to `du`, but very fast.
- Supports customizable rules to color files and assign icons based on folder names, file names, and file extensions, similar to `exa`, `eza`, `lsd`.
- Supports regex search for files or folders in a specified directory, similar to `find`, `fd`.

# Usage

### Special folders
- `.` Current folder
- `..` Parent folder
- `/` Root folder
- `~` Home folder

### List files
- `wf .` Display the file list of the current folder. 
- `wf ..` Display the file list of the parent folder.
- `wf /` Display the file list of the root folder.
- `wf ~` Display the file list of the home folder.
- `wf c:\folder` Display the file list of a specified folder.
- `wf c:\folder1,c:\folder2,c:\folder3` Display the file lists of specified multiple folders.
- `wf -d 3 c:\folder` Display a tree view of the specified folder, with a maximum depth of `3` levels. **The long option for `-d` is `--depth`.**
- `wf -d 3 c:\folder1,c:\folder2,c:\folder3d` Display the tree view of each specified folder, with a maximum depth of `3` levels.

### Calculate the folder size
- `wf -s c:\folder` Display the sizes of each subfolder in the specified folder. **The long option for `-s` is `--size`.**
- `wf -s -n 10 c:\folder` Display the top `10` largest subfolders in the specified folder. **The long option for `-n` is `--lines`.**
- `wf -s -d 3 -n 10 c:\folder` Display the top `10` largest subfolders in the specified folder with a maximum depth of `3` levels.
- `wf -s c:\folder1,c:\folder2,c:\folder3` Display the sizes of each subfolder in the specified multiple folders.
- `wf -s -n 10 c:\folder1,c:\folder2,c:\folder3` Display the top `10` largest subfolders in the specified multiple folders.
- `wf -s -d 3 -n 10 c:\folder1,c:\folder2,c:\folder3` Display the top `10` largest subfolders in the specified multiple folders with a maximum depth of `3` levels.

### Index and search files
- `wf -u` Update the index file, if it doesn't exist, create it. **The long option for `-u` is `--update`.**
- `wf -u c:\folder` Update the index for the specified folder, if it doesn't exist, create it.
- `wf . regex` Use `regex` to search for files in the current folder **without updating the index.**
- `wf -C . regex` Use `regex` to search for files in the current folder **with case insensitivity and without updating the index.** **The long option for `-C` is `--case-sensitive`.**
- `wf -u . regex` First update the index, then use `regex` to search for files in the current folder.
- `wf -u .,..,c:\folder regex1 regex2 regex3` First update the index, then search for files matching the `regex1`, `regex2` and `regex3` in the `current folder`, the `parent folder`, and `c:\folder`.
- `wf -u .,..,c:\folder regex1|regex2|regex3` First update the index, then search for files matching any of the `regex1`, `regex2` and `regex3` in the `current folder`, the `parent folder`, and `c:\folder`

Note: By default, **matches are case insensitive**.

Note: **`wf -u c:\folder regex` and `wf c:\folder regex -u` are equivalent**. If the previous command didn't find any files, simply append `-u` to update the index and search again, making it very convenient.

# Performance

The hardware used for generating the data in these benchmarks was

    windows 10 - 2.3 GHz Intel Core i5 and 8GB memory.

The version of clients:

| Application | Version | Release Date |
| --- | --- | --- |
| WindFind Birth | v1.0.0 | 2024-11-01 |
| Everything | v1.4.1.1024.x64 | 2023-05-26 |
| Everything | v1.5.0.1383a.x64 | 2024-06-17 |

**All test data is for reference only.**

### Disk C: NTFS File System

<table>
  <tr>
    <th></th>
    <th colspan="2">WindFind Birth</th>
    <th>Everything v1.4.1.1024.x64</th>
    <th>Everything v1.5.0.1383a.x64</th>
  </tr>
  <tr>
    <td>User Role</td>
    <td>Administrator</td>
    <td>Regular User</td>
    <td>Administrator</td>
    <td>Administrator</td>
  </tr>
  <tr>
    <td>Indexed File Count</td>
    <td>1561029</td>
    <td>1539637</td>
    <td>1561161</td>
    <td>1561160</td>
  </tr>
  <tr>
    <td>Indexed File Size</td>
    <td><strong>6.80 MiB (compressed)</strong></td>
    <td><strong>6.69 MiB (compressed)</strong></td>
    <td>13.2 MiB (compressed)<br>41.5 MiB (uncompressed)</td>
    <td>37.0 MiB (uncompressed)</td>
  </tr>
  <tr>
    <td>Create Index (Cold Data)</td>
    <td><strong>6.336s</strong></td>
    <td>10.20s</td>
    <td>87.12s</td>
    <td>10.25s</td>
  </tr>
  <tr>
    <td>Create Index (Hot Data)</td>
    <td><strong>4.314s</strong></td>
    <td>5.148s</td>
    <td>87.70s</td>
    <td>6.30s</td>
  </tr>
  <tr>
    <td>Update Index</td>
    <td>1.175s</td>
    <td>1.242s</td>
    <td><strong>Very fast, tens of ms</strong></td>
    <td><strong>Very fast, tens of ms</strong></td>
  </tr>
  <tr>
    <td>Load Index Duration</td>
    <td><strong>0.132s</strong></td>
    <td><strong>0.128s</strong></td>
    <td>Slow, 1s - 2s</td>
    <td>Slow, 1s - 2s</td>
  </tr>
  <tr>
    <td>Save Index Duration</td>
    <td><strong>0.155s</strong></td>
    <td><strong>0.148s</strong></td>
    <td>Slow, 1s - 4s</td>
    <td>Slow, 1s - 4s</td>
  </tr>
  <tr>
    <td>Single Regex Search Duration</td>
    <td>Very fast, 8ms - 12ms</td>
    <td>Very fast, 8ms - 12ms</td>
    <td>Very fast, tens of ms</td>
    <td>Very fast, tens of ms</td>
  </tr>
</table>

### Disk D: exFAT File System

**Note: Everything v1.4.1.1024.x64 does not support the exFAT file system.**

<table>
  <tr>
    <th></th>
    <th>WindFind Birth</th>
    <th>Everything v1.5.0.1383a.x64</th>
  </tr>
  <tr>
    <td>User Role</td>
    <td>Administrator, Regular User</td>
    <td>Administrator, Regular User</td>
  </tr>
  <tr>
    <td>Indexed File Count</td>
    <td>200758</td>
    <td>200757</td>
  </tr>
  <tr>
    <td>Indexed File Size</td>
    <td><strong>0.73 MiB (compressed)</strong></td>
    <td>4.1 MiB (uncompressed)</td>
  </tr>
  <tr>
    <td>Create Index (Cold Data)</td>
    <td><strong>1.566s</strong></td>
    <td>10.48s</td>
  </tr>
  <tr>
    <td>Create Index (Hot Data)</td>
    <td><strong>1.027s</strong></td>
    <td>1.38s</td>
  </tr>
  <tr>
    <td>Update Index</td>
    <td>1.055s</td>
    <td><strong>Very fast, tens of ms</strong></td>
  </tr>
  <tr>
    <td>Load Index Duration</td>
    <td><strong>20ms</strong></td>
    <td>Slow, several hundred milliseconds</td>
  </tr>
  <tr>
    <td>Save Index Duration</td>
    <td><strong>27ms</strong></td>
    <td>Slow, several hundred milliseconds</td>
  </tr>
  <tr>
    <td>Single Regex Search Duration</td>
    <td>Very fast, 8ms - 12ms</td>
    <td>Very fast, tens of ms</td>
  </tr>
</table>
