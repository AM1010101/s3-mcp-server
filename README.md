# S3 MCP Server

A Model Context Protocol server that interfaces with S3-compatible storage (like Cloudflare R2).

## Features

- List buckets (`s3_list_buckets`)
- List objects in a bucket (`s3_list_objects`)
- Read object content (`s3_read_object`)
- Upload objects (`s3_put_object`)
- Delete objects (`s3_delete_object`)

## Installation

1.  Navigate to the directory:
    ```bash
    cd s3-mcp-server
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Build the server:
    ```bash
    npm run build
    ```

## Configuration

To use this with an MCP client (like Claude Desktop or a custom client), add it to your configuration.

### Cloudflare R2 Example

For Cloudflare R2, your endpoint should look like: `https://<ACCOUNT_ID>.r2.cloudflarestorage.com`

#### Running from GitHub (Recommended)

```json
{
  "mcpServers": {
    "s3": {
      "command": "npx",
      "args": [
        "-y",
        "github:AM1010101/s3-mcp-server"
      ],
      "env": {
        "S3_ENDPOINT": "https://<YOUR_ACCOUNT_ID>.r2.cloudflarestorage.com",
        "S3_ACCESS_KEY_ID": "<YOUR_ACCESS_KEY_ID>",
        "S3_SECRET_ACCESS_KEY": "<YOUR_SECRET_ACCESS_KEY>",
        "S3_REGION": "auto"
      }
    }
  }
}
```

#### Running Locally

If you have cloned the repository and built it locally:

```json
{
  "mcpServers": {
    "s3": {
      "command": "node",
      "args": ["/absolute/path/to/s3-mcp-server/dist/index.js"],
      "env": {
        "S3_ENDPOINT": "https://<YOUR_ACCOUNT_ID>.r2.cloudflarestorage.com",
        "S3_ACCESS_KEY_ID": "<YOUR_ACCESS_KEY_ID>",
        "S3_SECRET_ACCESS_KEY": "<YOUR_SECRET_ACCESS_KEY>",
        "S3_REGION": "auto"
      }
    }
  }
}
```

### Environment Variables

- `S3_ENDPOINT`: The S3 API endpoint URL.
- `S3_ACCESS_KEY_ID`: Your access key ID.
- `S3_SECRET_ACCESS_KEY`: Your secret access key.
- `S3_REGION`: The region (default: "auto").

## Tools

- **s3_list_buckets**: Lists all available buckets.
- **s3_list_objects**: Lists files in a bucket.
  - `bucket`: Name of the bucket.
  - `prefix`: (Optional) Filter by prefix.
- **s3_read_object**: Reads a file as text.
  - `bucket`: Name of the bucket.
  - `key`: File path/key.
- **s3_put_object**: Uploads text content to a file.
  - `bucket`: Name of the bucket.
  - `key`: File path/key.
  - `content`: Content string.
- **s3_delete_object**: Deletes a file.
  - `bucket`: Name of the bucket.
  - `key`: File path/key.
