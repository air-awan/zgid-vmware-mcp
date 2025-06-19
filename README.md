# Zettagrid VMware MCP

A multi-project repository containing cloud infrastructure and development tools for VMware and CloudStack environments.

## Projects

This repository contains several independent projects:

- **`cloud-director-mcp/`** - VMware Cloud Director MCP Server (Multi-Zone support)
- **`cloudstack-mcp-server/`** - Apache CloudStack MCP Server with CLI interface  
- **`zettagrid-cloud-director-mcp/`** - Zettagrid-specific Cloud Director MCP Server
- **`cloudstack-enhanced-nas-backup/`** - Java-based CloudStack backup plugin
- **`markdown-viewer/`** - Tauri-based desktop markdown viewer application

## Getting Started

Each project has its own build system and dependencies. Navigate to the specific project directory and follow its README for setup instructions.

### TypeScript/Node.js Projects
```bash
cd <project-directory>
npm install
npm run build
npm start
```

### Java Project
```bash
cd cloudstack-enhanced-nas-backup/enhanced-nas-backup-plugin
mvn clean compile
mvn package
```

### Tauri Project
```bash
cd markdown-viewer
npm install
npm run tauri build
```

## Architecture

All MCP (Model Context Protocol) servers follow a consistent pattern with TypeScript implementations, API client libraries, and organized tool handlers.

## License

MIT