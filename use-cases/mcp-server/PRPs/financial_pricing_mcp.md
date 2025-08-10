---
name: "Financial Asset Pricing MCP Server"
description: This PRP provides comprehensive instructions for building a production-ready MCP server that calculates theoretical prices for US financial assets including stocks, bonds, and options, integrated with Yahoo Finance for market data.
---

## Purpose

Template for AI agents to implement a production-ready financial asset pricing MCP server with Yahoo Finance integration, theoretical pricing models, and comprehensive risk metrics, using GitHub OAuth authentication and Cloudflare Workers deployment.

## Core Principles

1. **Context is King**: Include ALL necessary financial pricing patterns, market data integration, and authentication flows
2. **Validation Loops**: Provide executable tests from TypeScript compilation to production deployment
3. **Security First**: Build-in authentication, authorization, and secure handling of financial data
4. **Production Ready**: Include monitoring, error handling, rate limiting, and deployment automation

---

## Goal

Build a production-ready MCP (Model Context Protocol) server with:

- Yahoo Finance integration for real-time and historical market data retrieval
- Black-Scholes and binomial options pricing models with full Greeks calculation
- Bond pricing with yield-to-maturity, duration, and convexity analysis
- Historical volatility calculation with configurable methods
- Risk-free rate management using current US Treasury rates
- Symbol validation and options chain data retrieval
- GitHub OAuth authentication with role-based access control
- Cloudflare Workers deployment with monitoring

## Why

- **Investment Analysis**: Enable AI assistants to provide accurate theoretical asset valuations
- **Risk Management**: Calculate comprehensive risk metrics (Greeks, duration, convexity) for portfolio analysis
- **Market Intelligence**: Access real-time and historical market data for informed decision-making
- **Enterprise Security**: GitHub OAuth ensures secure access to financial calculations
- **Scalability**: Cloudflare Workers provides global edge deployment for low-latency calculations
- **Accuracy**: Industry-standard pricing models ensure reliable valuations

## What

### MCP Server Features

**Core MCP Tools:**

- Tools are organized in modular files (one tool per file for maintainability)
- Each pricing model gets its own tool registration file
- Tools include comprehensive error handling and input validation
- All financial calculations maintain precision for currency amounts

**Financial Pricing Tools:**

1. **Stock Tools** (`stock-tools.ts`):
   - `getStockPrice` - Retrieve real-time stock prices and market metrics
   - `getHistoricalPrices` - Fetch historical price data with flexible time periods
   - `validateSymbol` - Validate trading symbols and get asset information

2. **Options Tools** (`options-tools.ts`):
   - `calculateBlackScholes` - Price options using Black-Scholes model
   - `calculateBinomial` - Price options using binomial tree model  
   - `calculateGreeks` - Compute full Greeks (Delta, Gamma, Theta, Vega, Rho)
   - `getOptionsChain` - Retrieve options chain data with strikes and IVs

3. **Bond Tools** (`bond-tools.ts`):
   - `calculateBondPrice` - Price bonds using yield-to-maturity
   - `calculateDuration` - Calculate Macaulay and modified duration
   - `calculateConvexity` - Compute bond convexity for risk analysis

4. **Market Data Tools** (`market-data-tools.ts`):
   - `calculateHistoricalVolatility` - Compute volatility using log returns
   - `getRiskFreeRate` - Fetch current US Treasury rates
   - `getMarketData` - Retrieve comprehensive market data

**Authentication & Authorization:**

- GitHub OAuth 2.0 integration with signed cookie approval system
- Role-based access control (read-only vs privileged users)
- Privileged users can access sensitive calculations and bulk data retrieval
- User context propagation to all MCP tools

**Data Integration:**

- Yahoo Finance API integration with rate limiting and caching
- Error handling for invalid symbols and API failures
- Time zone handling for market hours and timestamps
- Configurable data refresh intervals


### Success Criteria

- [ ] MCP server passes validation with MCP Inspector
- [ ] GitHub OAuth flow works end-to-end (authorization → callback → MCP access)
- [ ] TypeScript compilation succeeds with no errors
- [ ] Yahoo Finance integration retrieves accurate market data
- [ ] Black-Scholes calculations match reference implementations
- [ ] Bond pricing calculations are accurate within 0.01% tolerance
- [ ] Greeks calculations validated against industry benchmarks
- [ ] Error handling provides user-friendly messages for invalid inputs
- [ ] All financial calculations maintain 6 decimal place precision

## All Needed Context

### Documentation & References (MUST READ)

```yaml
# CRITICAL MCP PATTERNS - Read these first
- docfile: PRPs/ai_docs/mcp_patterns.md
  why: Core MCP development patterns, security practices, and error handling

# Critical code examples
- docfile: PRPs/ai_docs/claude_api_usage.md
  why: How to use the Anthropic API to get a response from an LLM

# TOOL REGISTRATION SYSTEM - Understand the modular approach
- file: src/tools/register-tools.ts
  why: Central registry showing how all tools are imported and registered - STUDY this pattern

# EXAMPLE MCP TOOLS - Look here how to create and register new tools
- file: examples/database-tools.ts
  why: Example tools for a Postgres MCP server showing best practices for tool creation and registration

- file: examples/database-tools-sentry.ts
  why: Example tools for the Postgres MCP server but with the Sentry integration for production monitoring

# EXISTING CODEBASE PATTERNS - Study these implementations
- file: src/index.ts
  why: Complete MCP server with authentication, database, and tools - MIRROR this pattern

- file: src/github-handler.ts
  why: OAuth flow implementation - USE this exact pattern for authentication

- file: src/database.ts
  why: Database security, connection pooling, SQL validation - ADAPT patterns for API rate limiting

- file: wrangler.jsonc
  why: Cloudflare Workers configuration - COPY this pattern for deployment

# OFFICIAL MCP DOCUMENTATION
- url: https://modelcontextprotocol.io/docs/concepts/tools
  why: MCP tool registration and schema definition patterns

- url: https://modelcontextprotocol.io/docs/concepts/resources
  why: MCP resource implementation if needed

# FINANCIAL PRICING REFERENCES
- url: https://github.com/lballabio/QuantLib
  why: Reference implementation for financial pricing models

- url: https://en.wikipedia.org/wiki/Black%E2%80%93Scholes_model
  why: Black-Scholes formula and Greeks calculation reference

- url: https://pypi.org/project/yfinance/
  why: Yahoo Finance API usage patterns and data structures
```

### Current Codebase Tree

```bash
/
├── src/
│   ├── index.ts                 # Main authenticated MCP server ← STUDY THIS
│   ├── index_sentry.ts         # Sentry monitoring version
│   ├── simple-math.ts          # Basic MCP example ← GOOD STARTING POINT
│   ├── github-handler.ts       # OAuth implementation ← USE THIS PATTERN
│   ├── database.ts             # Database utilities ← ADAPT FOR API CACHING
│   ├── utils.ts                # OAuth helpers
│   ├── workers-oauth-utils.ts  # Cookie security system
│   └── tools/                  # Tool registration system
│       └── register-tools.ts   # Central tool registry ← UNDERSTAND THIS
├── PRPs/
│   ├── templates/prp_mcp_base.md  # Base template
│   ├── financial_pricing_mcp.md   # This PRP
│   └── ai_docs/                   # Implementation guides ← READ ALL
├── examples/                   # Example tool implementations
│   ├── database-tools.ts       # Database tools example ← FOLLOW PATTERN
│   └── database-tools-sentry.ts # With Sentry monitoring
├── wrangler.jsonc              # Cloudflare config ← COPY PATTERNS
├── package.json                # Dependencies
└── tsconfig.json               # TypeScript config
```

### Desired Codebase Tree

```bash
/
├── src/
│   ├── financial-pricing.ts    # Main financial pricing MCP server
│   ├── financial-pricing-sentry.ts # With Sentry monitoring
│   └── tools/                  
│       ├── register-tools.ts   # Updated with financial tools
│       ├── stock-tools.ts      # Stock pricing and data tools
│       ├── options-tools.ts    # Options pricing and Greeks
│       ├── bond-tools.ts       # Bond pricing and risk metrics
│       └── market-data-tools.ts # Market data and volatility
├── lib/
│   ├── yahoo-finance.ts        # Yahoo Finance API wrapper
│   ├── pricing-models.ts       # Core pricing calculations
│   ├── risk-metrics.ts         # Greeks and risk calculations
│   └── utils/
│       ├── cache.ts            # API response caching
│       └── validators.ts       # Input validation utilities
├── types/
│   ├── financial.ts            # Financial data types
│   └── api.ts                  # API response types
├── wrangler-financial.jsonc    # Financial pricing Worker config
├── .dev.vars.example           # Updated with Yahoo Finance API key
└── tests/
    ├── pricing.test.ts         # Pricing model tests
    └── api.test.ts            # API integration tests
```

### Known Gotchas & Critical Financial Patterns

```typescript
// CRITICAL: Financial calculation patterns
// 1. ALWAYS validate numeric inputs for financial calculations
const PriceSchema = z.number().positive().finite();
const VolatilitySchema = z.number().min(0.0001).max(5); // 0.01% to 500%
const InterestRateSchema = z.number().min(-0.1).max(0.5); // -10% to 50%

// 2. ALWAYS handle market data errors gracefully
try {
  const data = await fetchMarketData(symbol);
} catch (error) {
  if (error.message.includes('Invalid symbol')) {
    return createErrorResponse(`Symbol '${symbol}' not found in market data`);
  }
  return createErrorResponse('Market data temporarily unavailable');
}

// 3. ALWAYS use precise decimal calculations
import { Decimal } from 'decimal.js';
const price = new Decimal(stockPrice);
const strike = new Decimal(strikePrice);

// 4. ALWAYS validate date inputs for options
const maturityDate = new Date(expiration);
if (maturityDate <= new Date()) {
  return createErrorResponse('Option expiration must be in the future');
}

// 5. ALWAYS implement rate limiting for API calls
const rateLimiter = new RateLimiter({
  maxRequests: 100,
  windowMs: 60000 // 1 minute
});

// 6. ALWAYS cache market data appropriately
const CACHE_DURATION = {
  realtime: 1000,      // 1 second for real-time quotes
  historical: 3600000, // 1 hour for historical data
  static: 86400000    // 24 hours for static data
};

// 7. Financial precision requirements
const formatPrice = (value: number): string => {
  return value.toFixed(6); // 6 decimal places for prices
};

const formatPercentage = (value: number): string => {
  return (value * 100).toFixed(4) + '%'; // 4 decimal places for percentages
};
```

## Implementation Blueprint

### Data Models & Types

Define TypeScript interfaces and Zod schemas for financial data validation.

```typescript
// types/financial.ts - Core financial types
export interface StockQuote {
  symbol: string;
  price: number;
  volume: number;
  marketCap: number;
  timestamp: Date;
}

export interface OptionContract {
  underlying: string;
  strike: number;
  expiration: Date;
  type: 'call' | 'put';
  price: number;
  impliedVolatility: number;
}

export interface BondData {
  faceValue: number;
  couponRate: number;
  maturity: Date;
  frequency: 1 | 2; // Annual or semi-annual
  yieldToMaturity: number;
}

export interface Greeks {
  delta: number;
  gamma: number;
  theta: number;
  vega: number;
  rho: number;
}

// Zod schemas for input validation
export const BlackScholesInputSchema = z.object({
  stockPrice: z.number().positive().describe("Current stock price"),
  strikePrice: z.number().positive().describe("Option strike price"),
  timeToExpiry: z.number().positive().describe("Time to expiration in years"),
  riskFreeRate: z.number().describe("Risk-free interest rate"),
  volatility: z.number().positive().describe("Implied or historical volatility"),
  optionType: z.enum(['call', 'put']).describe("Option type"),
});

export const BondPriceInputSchema = z.object({
  faceValue: z.number().positive().describe("Bond face value"),
  couponRate: z.number().min(0).max(1).describe("Annual coupon rate"),
  yieldToMaturity: z.number().describe("Yield to maturity"),
  yearsToMaturity: z.number().positive().describe("Years until maturity"),
  frequency: z.number().int().min(1).max(2).optional().describe("Payment frequency per year"),
});

export const MarketDataInputSchema = z.object({
  symbol: z.string().min(1).max(10).describe("Trading symbol"),
  period: z.enum(['1d', '5d', '1mo', '3mo', '6mo', '1y', '2y', '5y', 'max']).optional(),
  interval: z.enum(['1m', '5m', '15m', '30m', '1h', '1d', '1wk', '1mo']).optional(),
});

// Environment interface with Yahoo Finance API
interface Env {
  YAHOO_FINANCE_API_KEY?: string; // Optional, for premium features
  GITHUB_CLIENT_ID: string;
  GITHUB_CLIENT_SECRET: string;
  OAUTH_KV: KVNamespace;
  CACHE_KV: KVNamespace; // For market data caching
  COOKIE_ENCRYPTION_KEY: string;
}
```

### List of Tasks (Complete in order)

```yaml
Task 1 - Project Setup:
  COPY wrangler.jsonc to wrangler-financial.jsonc:
    - MODIFY name field to "financial-pricing-mcp"
    - ADD CACHE_KV to kv_namespaces bindings
    - ADD YAHOO_FINANCE_API_KEY to vars section (if using premium API)
    - KEEP existing OAuth and authentication configuration

  UPDATE .dev.vars.example:
    - ADD YAHOO_FINANCE_API_KEY=your_api_key_if_needed
    - KEEP all existing OAuth variables
    - ADD comment about Yahoo Finance rate limits

  INSTALL required dependencies:
    - RUN: npm install yfinance yahoo-finance2 decimal.js
    - RUN: npm install --save-dev @types/node

Task 2 - Core Library Implementation:
  CREATE lib/yahoo-finance.ts:
    - IMPLEMENT YahooFinanceClient class with rate limiting
    - ADD methods for getQuote, getHistoricalData, getOptionsChain
    - IMPLEMENT caching layer using KV storage
    - ADD comprehensive error handling for API failures

  CREATE lib/pricing-models.ts:
    - IMPLEMENT blackScholesPrice function with call/put options
    - IMPLEMENT binomialTreePrice function for American options
    - ADD helper functions for normal distribution calculations
    - ENSURE all calculations use Decimal.js for precision

  CREATE lib/risk-metrics.ts:
    - IMPLEMENT calculateDelta, calculateGamma functions
    - IMPLEMENT calculateTheta, calculateVega, calculateRho
    - ADD calculateImpliedVolatility using Newton-Raphson
    - IMPLEMENT bond duration and convexity calculations

  CREATE lib/utils/validators.ts:
    - IMPLEMENT validateSymbol function with asset type detection
    - ADD validateDateRange for historical data requests
    - CREATE validateFinancialInputs for numeric validation
    - ADD sanitizeSymbol to prevent injection attacks

Task 3 - MCP Server Implementation:
  CREATE src/financial-pricing.ts:
    - COPY class structure from src/index.ts
    - MODIFY server name to "Financial Asset Pricing MCP Server"
    - UPDATE version to "1.0.0"
    - IMPORT and initialize YahooFinanceClient
    - CALL registerAllTools(server, env, props) in init()

  CREATE src/financial-pricing-sentry.ts:
    - COPY from financial-pricing.ts
    - ADD Sentry initialization and instrumentation
    - WRAP all tool calls with Sentry spans
    - ADD financial-specific attributes to traces

Task 4 - Stock Tools Implementation:
  CREATE src/tools/stock-tools.ts:
    - EXPORT registerStockTools function
    - IMPLEMENT getStockPrice tool with real-time quote retrieval
    - IMPLEMENT getHistoricalPrices with configurable periods
    - IMPLEMENT validateSymbol with comprehensive validation
    - ADD permission checks for bulk data operations

Task 5 - Options Tools Implementation:
  CREATE src/tools/options-tools.ts:
    - EXPORT registerOptionsTools function
    - IMPLEMENT calculateBlackScholes with full validation
    - IMPLEMENT calculateBinomial for American options
    - IMPLEMENT calculateGreeks with all five Greeks
    - IMPLEMENT getOptionsChain with strike/expiry filtering
    - RESTRICT high-volume operations to privileged users

Task 6 - Bond Tools Implementation:
  CREATE src/tools/bond-tools.ts:
    - EXPORT registerBondTools function
    - IMPLEMENT calculateBondPrice with present value calculation
    - IMPLEMENT calculateDuration (Macaulay and modified)
    - IMPLEMENT calculateConvexity for interest rate risk
    - ADD support for zero-coupon and callable bonds

Task 7 - Market Data Tools:
  CREATE src/tools/market-data-tools.ts:
    - EXPORT registerMarketDataTools function
    - IMPLEMENT calculateHistoricalVolatility with log returns
    - IMPLEMENT getRiskFreeRate using Treasury data
    - IMPLEMENT getMarketData with comprehensive metrics
    - ADD caching for frequently accessed data

Task 8 - Tool Registry Update:
  MODIFY src/tools/register-tools.ts:
    - IMPORT all financial tool registration functions
    - ADD calls to register each tool category
    - MAINTAIN existing database tools if needed
    - ENSURE proper ordering of tool registration

Task 9 - Testing Implementation:
  CREATE tests/pricing.test.ts:
    - TEST Black-Scholes against known values
    - TEST bond pricing calculations
    - VALIDATE Greeks calculations
    - TEST edge cases (zero volatility, negative rates)

  CREATE tests/api.test.ts:
    - MOCK Yahoo Finance API responses
    - TEST error handling for invalid symbols
    - VALIDATE rate limiting behavior
    - TEST caching functionality

Task 10 - Environment Configuration:
  SETUP Cloudflare KV namespaces:
    - RUN: wrangler kv namespace create "OAUTH_KV"
    - RUN: wrangler kv namespace create "CACHE_KV"
    - UPDATE wrangler-financial.jsonc with namespace IDs

  SET production secrets:
    - RUN: wrangler secret put GITHUB_CLIENT_ID
    - RUN: wrangler secret put GITHUB_CLIENT_SECRET
    - RUN: wrangler secret put COOKIE_ENCRYPTION_KEY
    - RUN: wrangler secret put YAHOO_FINANCE_API_KEY (if using)

Task 11 - Local Testing:
  TEST financial calculations:
    - RUN: npm test
    - VERIFY all pricing tests pass
    - CHECK calculation precision

  TEST MCP server:
    - RUN: wrangler dev --config wrangler-financial.jsonc
    - TEST OAuth flow
    - VERIFY all tools respond correctly
    - TEST with MCP Inspector

```

### Per Task Implementation Details

```typescript
// Task 2 - Yahoo Finance Client Implementation
// lib/yahoo-finance.ts
import { z } from 'zod';

export class YahooFinanceClient {
  private cache: KVNamespace;
  private rateLimiter: RateLimiter;

  constructor(cache: KVNamespace) {
    this.cache = cache;
    this.rateLimiter = new RateLimiter({
      maxRequests: 100,
      windowMs: 60000
    });
  }

  async getQuote(symbol: string): Promise<StockQuote> {
    const cacheKey = `quote:${symbol}`;
    const cached = await this.cache.get(cacheKey, 'json');
    
    if (cached && Date.now() - cached.timestamp < 1000) {
      return cached.data;
    }

    await this.rateLimiter.checkLimit();
    
    try {
      // Implementation with Yahoo Finance API
      const quote = await fetchYahooQuote(symbol);
      
      await this.cache.put(cacheKey, JSON.stringify({
        data: quote,
        timestamp: Date.now()
      }), { expirationTtl: 60 });
      
      return quote;
    } catch (error) {
      throw new Error(`Failed to fetch quote for ${symbol}: ${error.message}`);
    }
  }
}

// Task 4 - Stock Tools Pattern
// src/tools/stock-tools.ts
export function registerStockTools(server: McpServer, env: Env, props: Props) {
  const yahooClient = new YahooFinanceClient(env.CACHE_KV);

  server.tool(
    "getStockPrice",
    "Get real-time stock price and market metrics",
    {
      symbol: z.string().min(1).max(10).describe("Stock symbol (e.g., AAPL)")
    },
    async ({ symbol }) => {
      try {
        const sanitized = sanitizeSymbol(symbol);
        const quote = await yahooClient.getQuote(sanitized);
        
        return {
          content: [{
            type: "text",
            text: `**Stock Quote: ${quote.symbol}**\n\n` +
                  `Price: $${quote.price.toFixed(2)}\n` +
                  `Volume: ${quote.volume.toLocaleString()}\n` +
                  `Market Cap: $${(quote.marketCap / 1e9).toFixed(2)}B\n` +
                  `Updated: ${quote.timestamp.toISOString()}`
          }]
        };
      } catch (error) {
        return createErrorResponse(`Failed to fetch stock price: ${error.message}`);
      }
    }
  );

  // Historical prices - available to all authenticated users
  server.tool(
    "getHistoricalPrices",
    "Fetch historical price data with flexible time periods",
    MarketDataInputSchema,
    async ({ symbol, period = '1mo', interval = '1d' }) => {
      try {
        const data = await yahooClient.getHistoricalData(symbol, period, interval);
        
        return {
          content: [{
            type: "text",
            text: `**Historical Data: ${symbol}**\n\n` +
                  `Period: ${period}, Interval: ${interval}\n` +
                  `Data Points: ${data.length}\n\n` +
                  `\`\`\`json\n${JSON.stringify(data.slice(0, 10), null, 2)}\n\`\`\``
          }]
        };
      } catch (error) {
        return createErrorResponse(`Failed to fetch historical data: ${error.message}`);
      }
    }
  );
}

// Task 5 - Options Pricing Implementation
// src/tools/options-tools.ts
const PRIVILEGED_TRADERS = new Set(['trader1', 'analyst1']);

export function registerOptionsTools(server: McpServer, env: Env, props: Props) {
  // Black-Scholes calculation - available to all
  server.tool(
    "calculateBlackScholes",
    "Calculate option price using Black-Scholes model",
    BlackScholesInputSchema,
    async ({ stockPrice, strikePrice, timeToExpiry, riskFreeRate, volatility, optionType }) => {
      try {
        const price = blackScholesPrice(
          stockPrice,
          strikePrice,
          timeToExpiry,
          riskFreeRate,
          volatility,
          optionType
        );
        
        return {
          content: [{
            type: "text",
            text: `**Black-Scholes Option Price**\n\n` +
                  `Type: ${optionType.toUpperCase()}\n` +
                  `Stock Price: $${stockPrice.toFixed(2)}\n` +
                  `Strike Price: $${strikePrice.toFixed(2)}\n` +
                  `Time to Expiry: ${timeToExpiry.toFixed(4)} years\n` +
                  `Volatility: ${(volatility * 100).toFixed(2)}%\n` +
                  `Risk-Free Rate: ${(riskFreeRate * 100).toFixed(2)}%\n\n` +
                  `**Theoretical Price: $${price.toFixed(6)}**`
          }]
        };
      } catch (error) {
        return createErrorResponse(`Black-Scholes calculation failed: ${error.message}`);
      }
    }
  );

  // Greeks calculation - available to all
  server.tool(
    "calculateGreeks",
    "Calculate option Greeks for risk analysis",
    BlackScholesInputSchema,
    async (params) => {
      try {
        const greeks = calculateAllGreeks(params);
        
        return {
          content: [{
            type: "text",
            text: `**Option Greeks**\n\n` +
                  `Delta: ${greeks.delta.toFixed(6)}\n` +
                  `Gamma: ${greeks.gamma.toFixed(6)}\n` +
                  `Theta: ${greeks.theta.toFixed(6)}\n` +
                  `Vega: ${greeks.vega.toFixed(6)}\n` +
                  `Rho: ${greeks.rho.toFixed(6)}`
          }]
        };
      } catch (error) {
        return createErrorResponse(`Greeks calculation failed: ${error.message}`);
      }
    }
  );

  // Options chain - restricted to privileged users
  if (PRIVILEGED_TRADERS.has(props.login)) {
    server.tool(
      "getOptionsChain",
      "Retrieve full options chain data (privileged)",
      {
        symbol: z.string(),
        expiration: z.string().optional()
      },
      async ({ symbol, expiration }) => {
        // Implementation for options chain retrieval
      }
    );
  }
}

// Task 3 - Main MCP Server
// src/financial-pricing.ts
export class FinancialPricingMCP extends McpAgent<Env, Record<string, never>, Props> {
  server = new McpServer({
    name: "Financial Asset Pricing MCP Server",
    version: "1.0.0",
  });

  async cleanup(): Promise<void> {
    // Cleanup any resources if needed
    console.log('Financial pricing MCP server cleanup completed');
  }

  async alarm(): Promise<void> {
    await this.cleanup();
  }

  async init() {
    console.log(`Financial pricing MCP server initialized for user: ${this.props.login}`);
    
    // Register all financial tools
    registerAllTools(this.server, this.env, this.props);
  }
}

// Export OAuth provider
export default new OAuthProvider({
  apiHandlers: {
    '/sse': FinancialPricingMCP.serveSSE('/sse') as any,
    '/mcp': FinancialPricingMCP.serve('/mcp') as any,
  },
  authorizeEndpoint: "/authorize",
  clientRegistrationEndpoint: "/register",
  defaultHandler: GitHubHandler as any,
  tokenEndpoint: "/token",
});
```

### Integration Points

```yaml
CLOUDFLARE_WORKERS:
  - wrangler-financial.jsonc: Configure for financial pricing server
  - KV namespaces: OAUTH_KV for auth, CACHE_KV for market data
  - Environment secrets: GitHub OAuth, Yahoo Finance API key
  - Durable Objects: MCP agent state persistence

YAHOO_FINANCE_INTEGRATION:
  - API endpoint: Use yahoo-finance2 npm package
  - Rate limiting: 100 requests per minute (free tier)
  - Caching strategy: 1s for quotes, 1h for historical data
  - Error handling: Symbol validation, network failures

AUTHENTICATION:
  - GitHub OAuth: Same pattern as database example
  - Privileged users: Define list for options chain access
  - Session management: Cookie-based approval system

FINANCIAL_CALCULATIONS:
  - Precision: Use Decimal.js for all calculations
  - Validation: Strict input validation for all parameters
  - Error bounds: Reasonable limits on volatility, rates
  - Time zones: Handle market hours correctly
```

## Validation Gate

### Level 1: TypeScript & Configuration

```bash
# CRITICAL: Run these FIRST - fix any errors before proceeding
npm run type-check                 # TypeScript compilation
wrangler types --config wrangler-financial.jsonc  # Generate types

# Expected: No TypeScript errors
# If errors: Fix type issues, missing interfaces, import problems
```

### Level 2: Unit Testing

```bash
# Run financial calculation tests
npm test

# Test specific pricing models
npm test -- pricing.test.ts

# Expected: All tests pass with correct calculations
# If failures: Verify formulas, check precision, fix edge cases
```

### Level 3: Local Development Testing

```bash
# Start local development server
wrangler dev --config wrangler-financial.jsonc

# Test OAuth flow
curl -v http://localhost:8792/authorize

# Test stock price tool
curl -X POST http://localhost:8792/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "method": "tools/call",
    "params": {
      "name": "getStockPrice",
      "arguments": {"symbol": "AAPL"}
    }
  }'

# Test Black-Scholes calculation
curl -X POST http://localhost:8792/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "method": "tools/call",
    "params": {
      "name": "calculateBlackScholes",
      "arguments": {
        "stockPrice": 100,
        "strikePrice": 110,
        "timeToExpiry": 0.25,
        "riskFreeRate": 0.05,
        "volatility": 0.3,
        "optionType": "call"
      }
    }
  }'

# Expected: Server starts, OAuth works, calculations return correct values
# If errors: Check environment variables, API keys, calculation logic
```

### Level 4: MCP Inspector Testing

```bash
# Test with MCP Inspector
npx @modelcontextprotocol/inspector@latest

# Add local server configuration
# Test each tool systematically
# Verify response formats

# Expected: All tools discoverable and functional
# If errors: Check tool registration, schema definitions
```

### Level 5: Production Deployment Testing

```bash
# Deploy to staging
wrangler deploy --env staging --config wrangler-financial.jsonc

# Test production OAuth flow
# Test with real market data
# Monitor performance and errors

# Expected: Deployment successful, all features working
# If errors: Check secrets configuration, API limits
```

## Final Validation Checklist

### Core Functionality

- [ ] TypeScript compilation: `npm run type-check` passes
- [ ] Unit tests pass: `npm test` successful
- [ ] Local server starts: `wrangler dev` runs without errors
- [ ] MCP endpoint responds: Returns server info correctly
- [ ] OAuth flow works: Authentication completes successfully

### Financial Features

- [ ] Stock price retrieval: Real-time quotes accurate
- [ ] Historical data: Time series data correctly formatted
- [ ] Black-Scholes pricing: Matches reference calculations
- [ ] Greeks calculation: All five Greeks computed correctly
- [ ] Bond pricing: Present value calculations accurate
- [ ] Volatility calculation: Historical volatility correct

### Production Readiness

- [ ] Error handling: Invalid symbols handled gracefully
- [ ] Rate limiting: API calls respect limits
- [ ] Caching: Market data cached appropriately
- [ ] Monitoring: Logs capture key events
- [ ] Security: Financial data access controlled
- [ ] Performance: Calculations complete quickly

---

## Anti-Patterns to Avoid

### Financial Calculation Specific

- ❌ Don't use floating-point arithmetic directly - use Decimal.js
- ❌ Don't ignore time zone differences for market data
- ❌ Don't cache sensitive pricing data too long
- ❌ Don't expose raw API errors to users

### MCP Development

- ❌ Don't skip input validation with Zod schemas
- ❌ Don't forget rate limiting for external APIs
- ❌ Don't hardcode financial constants - make configurable
- ❌ Don't ignore precision requirements for currency

### Security & Compliance

- ❌ Don't log sensitive financial data in production
- ❌ Don't allow unrestricted bulk data access
- ❌ Don't skip symbol validation - prevent injection
- ❌ Don't expose internal calculation errors

This PRP provides comprehensive guidance for building a production-ready financial asset pricing MCP server with theoretical pricing models, market data integration, and enterprise-grade security.