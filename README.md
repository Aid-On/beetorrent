# beetorrent

<div align="left">
  <img width="400px" src="https://github.com/user-attachments/assets/2b24c30c-b5f9-4cf6-9bc5-24eb0cd3a6e0">
</div>

## What is Beetorrent?

**Beetorrent** is a powerful frontend library designed for efficiently uploading large-scale and massive data files to **Google Cloud Platform (GCP)**. Leveraging GCP's **resumable upload** functionality, it ensures reliable uploads even in the face of network interruptions or disruptions. Designed to run in the frontend layer, such as in Next.js applications, Beetorrent is also built with extensibility in mind, paving the way for support for platforms like **AWS S3** and **Azure Blob Storage** in the future.

### Key Features

- **GCP Integration**: Direct support for GCP storage with resumable upload functionality.
- **Large File Support**: Efficiently handles massive data uploads.
- **Resumable Uploads**: Continue uploads seamlessly from where they left off after interruptions.
- **Streaming and Chunking**: Splits data into manageable chunks for better performance and error handling.
- **Next.js Compatibility**: Works smoothly in frontend environments.
- **Extensibility**: Future support for AWS S3, Azure Blob Storage, and other platforms is planned.

---

## Installation

Install Beetorrent with the following command:

```bash
npm install beetorrent
# or
yarn add beetorrent
```

---

## Usage Example

Here is an example of using Beetorrent to upload multiple files to GCP:

```typescript
import { Beetorrent } from 'beetorrent';

// Initialize Beetorrent instance
const beetorrent = new Beetorrent({
  provider: 'gcp',
  credentials: {
    projectId: 'your-gcp-project-id',
    clientEmail: 'your-gcp-service-account-email',
    privateKey: 'your-gcp-private-key',
  },
  bucketName: 'your-gcp-bucket',
});

// Upload multiple files from the frontend
async function uploadFiles(files: File[]) {
  try {
    const responses = await beetorrent.uploadFiles(files, {
      resumable: true, // Enable resumable uploads
    });

    console.log('All files uploaded successfully:', responses);
  } catch (error) {
    console.error('Error during upload:', error);
  }
}

// Trigger upload on file selection event
const fileInput = document.getElementById('file-input') as HTMLInputElement;
fileInput.addEventListener('change', (event) => {
  const files = Array.from((event.target as HTMLInputElement).files || []);
  uploadFiles(files);
});
```

---

## Why Choose Beetorrent?

Beetorrent simplifies the complexities of uploading large files to cloud platforms. By utilizing GCP's resumable upload feature, it ensures that uploads can resume from the point of interruption. Additionally, it works seamlessly in frontend environments like Next.js and supports batch processing for multiple files.

---

## Future Plans

- **Batch Uploads**:

  - Enable uploading multiple files together, in addition to single file uploads.

- **Resumable Uploads**:

  - For example, if 500MB of a 1GB file has been uploaded, the upload can resume from the remaining portion.
  - Utilize GCP's built-in mechanisms.

- **Support for Other Cloud Platforms**:

  - Provide extensibility for easy switching to AWS S3 or Azure Blob Storage.

---

## License

Beetorrent is licensed under the **Apache License 2.0**. See the [LICENSE](./LICENSE) file for details.

