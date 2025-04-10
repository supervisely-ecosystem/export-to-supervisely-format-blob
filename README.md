<div align="center" markdown>
<img src="https://github.com/supervisely-ecosystem/export-to-supervisely-format/releases/download/v3.2.6/poster_blob.png"/>

# Export to Supervisely format: Blob

<p align="center">
  <a href="#Overview">Overview</a> •
  <a href="#Format-Description">Format Description</a> •
  <a href="#How-To-Use">How To Use</a>
</p>

[![](https://img.shields.io/badge/supervisely-ecosystem-brightgreen)](https://ecosystem.supervisely.com/apps/supervisely-ecosystem/export-to-supervisely-format-blob)
[![](https://img.shields.io/badge/slack-chat-green.svg?logo=slack)](https://supervisely.com/slack)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/supervisely-ecosystem/export-to-supervisely-format-blob)
[![views](https://app.supervisely.com/img/badges/views/supervisely-ecosystem/export-to-supervisely-format-blob.png)](https://supervisely.com)
[![runs](https://app.supervisely.com/img/badges/runs/supervisely-ecosystem/export-to-supervisely-format-blob.png)](https://supervisely.com)

</div>

# Overview

Download images project or dataset in [extended Supervisely JSON format](https://docs.supervisely.com/customization-and-integration/00_ann_format_navi/01_project_structure_new) with blob storage optimization.

# Format Description

Supervisely provides a powerful optimization for projects containing a large number of small image files through its blob file system. Instead of handling thousands of individual files (which can lead to significant overhead in network transfers and filesystem operations), blob files consolidate many images into a single large binary file. This approach dramatically improves upload and download speeds, especially when dealing with datasets containing tens or hundreds of thousands of images.

## Project Structure

A typical exported project with blob storage has the following structure:

```
📂 project-name
 ┣ 📂 blob
 ┃  ┗ 📦 small_images.tar
 ┣ 📂 dataset-name-001
 ┃  ┣ 📄 small_images_offsets.pkl
 ┃  ┣ 📂 ann
 ┃  ┃  ┣ 📄 small-image-0000001.png.json
 ┃  ┃  ┣ ...
 ┃  ┃  ┗ 📄 small-image-0999999.png.json
 ┗ 📄 meta.json
```

The blob files work alongside offset files (with suffix `_offsets.pkl`), which store metadata about each image's location within the blob. These offset files contain information that defines the byte range representing each image in the binary, enabling efficient extraction without scanning the entire archive.

#### This approach provides:

-   Faster import and export speeds
-   Reduced server load
-   More efficient storage on disk
-   Minimized filesystem overhead when dealing with many small files

# How To Use

#### There are 2 ways how to export project:

1.  Run from the context menu → `Download` → `Export to Supervisely Format: Blob`

    <img src="https://placeholder.png">

2.  Run from the App Ecosystem

Result archive will be available for download in `Tasks` list (image below) or from `Team Files` (path format is the following `Files` → `tmp` → `supervisely` → `export` → `Export to Supervisely Format: Blob` → `<task_id>` → `<projectId>_<projectName>.tar`)

<img src="https://placeholder.png">
