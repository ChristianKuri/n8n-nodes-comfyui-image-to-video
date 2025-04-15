![Banner image](https://user-images.githubusercontent.com/10284570/173569848-c624317f-42b1-45a6-ab09-f0ea3c247648.png)

# n8n-nodes-comfyui

This package provides n8n nodes to integrate with [ComfyUI](https://github.com/comfyanonymous/ComfyUI) - A powerful and modular stable diffusion GUI with a graph/nodes interface.

## Features

- Execute ComfyUI workflows directly from n8n
- Generate images and videos using stable diffusion models
- Support for workflow JSON import
- Automatic output retrieval from workflow outputs
- Progress monitoring and error handling
- Support for API key authentication
- Configurable timeout settings

## Prerequisites

- n8n (version 1.0.0 or later)
- ComfyUI instance running and accessible
- Node.js 16 or newer

## Installation

```bash
npm install n8n-nodes-comfyui
```

## Node Types

### ComfyUI Node

This node allows you to execute ComfyUI workflows and retrieve generated images.

#### Settings

- **API URL**: The URL of your ComfyUI instance (default: http://127.0.0.1:8188)
- **API Key**: Optional API key if authentication is enabled
- **Workflow JSON**: The ComfyUI workflow in JSON format

#### Outputs

The node outputs an array of generated images with:
- `filename`: Name of the generated image file
- `subfolder`: Subfolder path if any
- `data`: Base64 encoded image data

### ComfyUI Image to Video Node

This node allows you to convert images to videos using ComfyUI's image-to-video capabilities (like AnimateDiff, WanImageToVideo, or video generation models).

#### Settings

- **API URL**: The URL of your ComfyUI instance (default: http://127.0.0.1:8188)
- **API Key**: Optional API key if authentication is enabled
- **Workflow JSON**: The ComfyUI workflow in JSON format for video generation
- **Input Type**: Choose between URL, Base64, or Binary input methods
- **Input Image**: URL or base64 string of the input image (when using URL or Base64 input type)
- **Binary Property**: Name of the binary property containing the image (when using Binary input type)
- **Timeout**: Maximum time in minutes to wait for video generation

#### Input

The node accepts an image input in three ways:
1. **URL**: Provide a direct URL to an image
2. **Base64**: Provide a base64-encoded image string
3. **Binary**: Use an image from a binary property in the workflow (e.g., from an HTTP Request node)

#### Outputs

The node outputs the generated video:
- In the `binary.data` property with proper MIME type and file information
- `fileName`: Name of the generated video file
- `data`: Base64 encoded video data
- `fileType`: The type of video file (e.g., 'video')
- `fileSize`: Size of the video in KB
- `fileExtension`: File extension (webp, mp4, gif)
- `mimeType`: MIME type of the video

## Usage Examples

### Using the ComfyUI Node

1. Export your workflow from ComfyUI as JSON
2. Create a new workflow in n8n
3. Add the ComfyUI node
4. Paste your workflow JSON
5. Configure the API URL
6. Execute and retrieve generated images

### Using the ComfyUI Image to Video Node

1. Create a workflow in ComfyUI for video generation (e.g., using WanImageToVideo, VHS_VideoCombine)
2. Export the workflow as JSON (API)
4. Add the ComfyUI Image to Video node
5. Paste your workflow JSON
6. Select the appropriate Input Type:
   - For URL: Enter the image URL
   - For Base64: Provide a base64 string
   - For Binary: Specify the binary property containing the image (default: "data")
7. Configure timeout as needed
8. Execute the workflow to generate a video from your input image

## Error Handling

The node includes comprehensive error handling for:
- API connection issues
- Invalid workflow JSON
- Execution failures
- Timeout conditions
- Input image validation

## Development

```bash
# Install dependencies
npm install

# Build
npm run build

# Test
npm run test

# Lint
npm run lint
```

## License

[MIT](LICENSE.md)
 