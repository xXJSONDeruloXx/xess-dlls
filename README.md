# XeSS DLLs Extractor

This repository automatically extracts and releases the core DLL files from Intel's XeSS (Xe Super Sampling) SDK.

## Overview

Intel XeSS is a temporal upscaling technology that uses machine learning to increase performance in games. This repository provides an automated way to extract just the essential DLL files from the full XeSS SDK releases.

## Extracted DLLs

The workflow extracts these 4 core DLL files from the XeSS SDK:

- **libxell.dll** - XeSS Low Latency library
- **libxess.dll** - XeSS Super Resolution core library  
- **libxess_dx11.dll** - XeSS DirectX 11 implementation
- **libxess_fg.dll** - XeSS Frame Generation library

## Usage

### Manual Trigger

1. Go to the [Actions](../../actions) tab
2. Select "Extract XeSS DLLs" workflow
3. Click "Run workflow" button
4. The workflow will automatically:
   - Download XeSS SDK v2.1.0 from Intel's GitHub releases
   - Verify the download checksum
   - Extract the required DLL files
   - Calculate SHA256 hashes for each DLL
   - Create a new release with timestamp-based tag
   - Upload all 4 DLL files as release assets

### Release Format

Each release includes:

- **Tag**: Timestamp in format `YYYYMMDD-HHMMSS` (UTC)
- **Title**: `XeSS DLLs YYYYMMDD-HHMMSS`
- **Description**: Contains links to source SDK and workflow run, plus JSON metadata
- **Assets**: The 4 extracted DLL files

### JSON Metadata

Each release description includes a JSON block with download URLs and SHA256 hashes:

```json
{
  "remote_binary": [
    {
      "name": "libxell.dll",
      "url": "https://github.com/username/repo/releases/download/TAG/libxell.dll",
      "sha256hash": "abc123..."
    },
    {
      "name": "libxess.dll", 
      "url": "https://github.com/username/repo/releases/download/TAG/libxess.dll",
      "sha256hash": "def456..."
    },
    {
      "name": "libxess_dx11.dll",
      "url": "https://github.com/username/repo/releases/download/TAG/libxess_dx11.dll", 
      "sha256hash": "ghi789..."
    },
    {
      "name": "libxess_fg.dll",
      "url": "https://github.com/username/repo/releases/download/TAG/libxess_fg.dll",
      "sha256hash": "jkl012..."
    }
  ]
}
```

## Source

The DLLs are extracted from:
- **Source**: [Intel XeSS v2.1.0](https://github.com/intel/xess/releases/tag/v2.1.0)
- **Original Archive**: `XeSS_SDK_2.1.0.zip`
- **Verified SHA256**: `dbcd513934c8b9b4aa7ae6897c57ce16110ca4dcb229fe6f45a9b6d4dac18253`

## Workflow Details

The GitHub Actions workflow:

1. **Downloads** the XeSS SDK v2.1.0 zip file
2. **Verifies** the SHA256 checksum matches the expected value
3. **Extracts** the zip file 
4. **Copies** only the 4 required DLL files from `bin/` directory
5. **Calculates** SHA256 hashes for each DLL
6. **Creates** a release with timestamp-based tag
7. **Uploads** each DLL as a release asset
8. **Generates** release description with source links and JSON metadata

## License

This repository contains workflow automation only. The extracted DLL files are subject to Intel's XeSS SDK license terms. 

**Important**: These DLL files are distributed under the **Intel Simplified Software License (Version October 2022)**. The license file (`INTEL_LICENSE.txt`) is included in:
- This repository
- Every release as a separate download
- The ZIP archive containing all DLLs

By downloading and using these DLL files, you agree to comply with Intel's license terms. Please refer to the [original XeSS repository](https://github.com/intel/xess) for additional information.

### Key License Requirements:
- Redistributions must include the copyright notice and license terms
- No reverse engineering, decompilation, or disassembly permitted
- No modification or alteration of the software allowed
- Software provided "as is" without warranty
