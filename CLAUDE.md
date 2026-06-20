# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Structure

This is a Zettagrid Indonesia VMware MCP (Model Context Protocol) Server that provides comprehensive tenant organization management across Indonesian zones. It's a TypeScript-based Node.js application that interfaces with VMware vCloud Director APIs.

### Core Architecture
- **`src/index.ts`** - Main MCP server entry point
- **`src/server/mcp-server.ts`** - MCP protocol implementation and tool handlers
- **`src/client/zettagrid-client.ts`** - Main API client with comprehensive vCloud Director operations
- **`src/managers/`** - Business logic and resource management
  - **`zone-manager.ts`** - Multi-zone configuration and management (Jakarta, Cibitung)
  - **`firewall-manager.ts`** - Firewall rule management and operations
  - **`vm-creator.ts`** - Virtual machine creation and lifecycle management
- **`src/auth/`** - Authentication system with OAuth token management
  - **`token-manager.ts`** - API token authentication and session management
  - **`zone-auth.ts`** - Zone-specific authentication handlers
- **`src/types.ts`** - Complete TypeScript interfaces for vCloud Director API schema
- **`src/utils/xml-parser.ts`** - XML response parsing utilities for vCloud Director API
- **`src/examples/`** - Example scripts and usage demonstrations
- **`src/lib/`** - Library exports for external usage

### Multi-Zone Support
The application supports Zettagrid Indonesia zones:
- **Jakarta** (zone code: `jkt`) — `https://mycloud-jkt.zettagrid.id/api`
- **Cibitung** (zone code: `cbt`) — `https://mycloud-cbt.zettagrid.id/api`

Each zone has independent authentication and API endpoints. Zone-aware session management and API routing is handled automatically.

## Build Commands

```bash
# Development
npm run dev              # Run in development mode with tsx
npm run build            # Compile TypeScript to build/
npm start                # Run compiled server

# Testing
npm test                 # Run Jest unit tests
npm run test:watch       # Run tests in watch mode
npm run test:coverage    # Run tests with coverage

# Code Quality
npm run lint             # Run ESLint
npm run lint:fix         # Fix ESLint issues

# Utilities
npm run clean            # Clean build directory
```

### Test Infrastructure
- **Unit tests**: Located in `tests/unit/`
- **Integration tests**: Located in `tests/integration/`
- **Live testing**: `npx tsx src/examples/connectivity-test.ts` - Tests against real Zettagrid infrastructure
- **Test fixtures**: Located in `tests/fixtures/`

## Environment Configuration

The application requires `.env` file with zone-specific credentials:

```bash
# Organization Configuration
ZETTAGRID_ORGANIZATION=your-organization-name
ZETTAGRID_DEFAULT_ZONE=jakarta
ZETTAGRID_API_VERSION=39.1

# Zone API Tokens (configure the zones you need)
ZETTAGRID_API_TOKEN_JAKARTA=your-jakarta-token
ZETTAGRID_API_TOKEN_CIBITUNG=your-cibitung-token

# Performance Settings (optional)
ZETTAGRID_TIMEOUT=30000
ZETTAGRID_RETRY_ATTEMPTS=3
ZETTAGRID_ENABLE_CACHING=true
DEBUG_LEVEL=info
```

**Note**: API and OAuth endpoints are automatically generated using the standard Zettagrid Indonesia format:
- API: `https://mycloud-{zone-code}.zettagrid.id/api`
- OAuth: `https://mycloud-{zone-code}.zettagrid.id/oauth/tenant/{org}/token`

Zone codes: Jakarta (`jkt`), Cibitung (`cbt`)

## Key Technologies

- **TypeScript 5.3+** - Strict typing with comprehensive vCloud Director schema compliance
- **Node.js 18+** - ES modules (`"type": "module"`)
- **MCP Protocol** - Model Context Protocol for AI assistant integration
- **axios** - HTTP client for vCloud Director API communication
- **zod** - Runtime schema validation
- **Jest** - Testing framework with TypeScript support
- **tsx** - TypeScript execution for development

## Authentication Architecture

### OAuth Flow Implementation
1. **API Token**: Initial Zettagrid API token per zone
2. **Token Exchange**: Automatic exchange for OAuth access tokens via `zettagrid.id` OAuth endpoint
3. **Session Management**: Cached sessions with automatic refresh
4. **Multi-Zone**: Independent authentication state per zone

### Authentication Classes
- `TokenManager` - Handles token lifecycle and session caching
- `ZoneAuth` - Zone-specific authentication operations
- `ZoneManager` - Configuration and zone discovery

## API Capabilities

The MCP server provides 20 tools for vCloud Director operations:

### Organization Management
- `list_organizations` - List all accessible organizations
- `get_organization` - Get organization details

### Virtual Data Center (VDC) Operations
- `list_vdcs` - List VDCs in an organization
- `get_vdc` - Get VDC details
- `show_vdc_resources` - Show VDC resource usage table (RAM, vCPU, Storage)
- `show_all_vdc_resources` - Consolidated resource table across all VDCs

### vApp and VM Management
- `list_vapps` - List virtual applications
- `list_vms` - List virtual machines
- `power_on_vm` - Power on a VM
- `power_off_vm` - Power off a VM
- `get_vm_console` - Get VM console access ticket

### Network and Security
- `list_edge_gateways` - List edge gateways
- `get_edge_gateway` - Get edge gateway details
- `list_firewall_rules` - List firewall rules
- `create_firewall_rule` - Create a firewall rule
- `show_edge_network_config` - Show edge network configuration
- `list_external_networks` - List external networks
- `get_provider_network_info` - Get provider network info

### Zone Management
- `test_zone` - Test connectivity and auth for a zone
- `get_zone_info` - Get zone configuration info

## Security Considerations

- All API credentials stored in environment variables only
- OAuth token refresh flow with secure session management
- SSL/TLS enforcement for all API communications
- Zone-isolated authentication to prevent cross-zone access
- No credentials stored in code or committed to repository
