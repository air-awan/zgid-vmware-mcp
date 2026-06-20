# Zettagrid Indonesia MCP Server - Example Scripts

This directory contains example scripts for testing and demonstrating the Zettagrid Indonesia MCP Server.

## Prerequisites

Create a `.env` file in the project root:

```bash
ZETTAGRID_ORGANIZATION=your-organization-name
ZETTAGRID_DEFAULT_ZONE=jakarta
ZETTAGRID_API_VERSION=39.1

# Zone API Tokens (configure the zones you need)
ZETTAGRID_API_TOKEN_JAKARTA=your-jakarta-api-token
ZETTAGRID_API_TOKEN_CIBITUNG=your-cibitung-api-token

ZETTAGRID_TIMEOUT=30000
ZETTAGRID_RETRY_ATTEMPTS=3
ZETTAGRID_ENABLE_CACHING=true
```

**Note**: Endpoints are automatically generated:
- API: `https://mycloud-jkt.zettagrid.id/api` (Jakarta)
- OAuth: `https://mycloud-jkt.zettagrid.id/oauth/tenant/{org}/token` (Jakarta)
- API: `https://mycloud-cbt.zettagrid.id/api` (Cibitung)
- OAuth: `https://mycloud-cbt.zettagrid.id/oauth/tenant/{org}/token` (Cibitung)

## Available Scripts

| Script | Description |
|--------|-------------|
| `connectivity-test.ts` | Test basic connectivity and authentication |
| `comprehensive-test.ts` | Full suite of API operations |
| `live-test.ts` | Live infrastructure discovery test |
| `live-test-scenario.ts` | End-to-end scenario test |
| `vm-power-test.ts` | VM power on/off operations |
| `test-vdc-resources.ts` | VDC resource reporting |
| `test-all-tools.ts` | Test all MCP tools |
| `test-available-tools.ts` | List and verify available tools |
| `test-firewall-tools.ts` | Firewall rule management |
| `test-vm-console.ts` | VM console access |
| `firewall-test.ts` | Firewall connectivity test |
| `firewall-investigation.ts` | Investigate firewall endpoints |
| `gateway-config-analyzer.ts` | Analyze edge gateway configuration |
| `debug-list-vdcs.ts` | Debug VDC listing |
| `debug-vdc-data.ts` | Debug VDC data retrieval |

## Running Examples

```bash
# Connectivity test
npx tsx src/examples/connectivity-test.ts

# Full live test
npx tsx src/examples/live-test.ts

# VM power operations
npx tsx src/examples/vm-power-test.ts

# Test all tools
npx tsx src/examples/test-all-tools.ts
```
