# Installation Guide

## Prerequisites

Before installing Metaclass, ensure you have the following prerequisites:

- Node.js (version 18.0 or higher)
- npm or yarn package manager
- TypeScript compiler (version 5.0 or higher)
- Git for version control

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/Oasis-Company/Metaclass.git
cd Metaclass
```

### 2. Install Dependencies

```bash
npm install
# or
yarn install
```

### 3. Build the Project

```bash
npm run build
# or
yarn build
```

### 4. Verify Installation

Run the following command to verify that the installation was successful:

```bash
npm run test
# or
yarn test
```

## Configuration

### Environment Variables

Metaclass requires the following environment variables to be set:

- `METACLASS_REGISTRY_URL`: URL of the Axis registry
- `METACLASS_CACHE_DIR`: Directory for caching constraint bundles
- `METACLASS_PROJECTION_DIR`: Directory for projection operators

### Configuration File

Create a `metaclass.config.json` file in the project root with the following structure:

```json
{
  "registry": {
    "url": "https://registry.metaclass.org"
  },
  "cache": {
    "dir": "./cache"
  },
  "projections": {
    "dir": "./projections"
  }
}
```

## Troubleshooting

### Common Issues

1. **Dependency Errors**: If you encounter dependency errors, try clearing the npm/yarn cache and reinstalling dependencies.

2. **Build Failures**: Ensure you have the correct TypeScript version installed.

3. **Registry Connection Issues**: Verify that the `METACLASS_REGISTRY_URL` is correct and accessible.

## Next Steps

Once installed, refer to the [Usage Guide](usage-guide.md) for information on how to use Metaclass in your projects.
