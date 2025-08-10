## FEATURE:

We want to create an MCP server that calculates theoretical prices for US financial assets including stocks, bonds, and options. The server integrates with Yahoo Finance for market data retrieval and implements theoretical pricing models to provide accurate asset valuations for investment analysis and decision-making.

Additional features:

- Black-Scholes and binomial options pricing models with full Greeks calculation
- Bond pricing using yield-to-maturity and present value models with duration and convexity
- Historical volatility calculation for options pricing inputs
- Risk-free rate management using current US Treasury rates
- Real-time and historical market data integration via Yahoo Finance API
- Symbol validation and options chain data retrieval

We need:

- To retrieve real-time stock prices and market metrics for US-listed equities
- To calculate theoretical bond prices with duration and convexity analysis
- To price options using industry-standard models with complete risk metrics
- To fetch comprehensive market data with flexible time periods and intervals
- To access current risk-free rates for accurate pricing model inputs
- To compute historical volatility for options pricing with configurable methods
- To validate trading symbols and retrieve detailed asset information
- To access options chain data with strike prices and implied volatilities

## EXAMPLES & DOCUMENTATION:

All examples are already referenced in prp_mcp_base.md - do any additional research as needed.

Examples and documentations on financial pricing : https://github.com/lballabio/QuantLib

Additional documentation should reference:
- Yahoo Finance API integration patterns
- Black-Scholes model implementation examples
- Bond pricing calculation methodologies
- Options Greeks calculation formulas

## OTHER CONSIDERATIONS:
- Do not use complex regex or complex parsing patterns, we use an LLM to parse PRPs.
- all API key need to be environment variables - these are set up in .dev.vars.example
- Use Yahoo Finance API for all market data retrieval - API key may be required depending on usage limits
- Implement robust error handling for invalid symbols and market data failures
- Risk-free rate should default to appropriate Treasury maturity based on option expiration
- Historical volatility calculations should use logarithmic returns for accuracy
- Bond pricing should handle both annual and semi-annual coupon payments
- Options pricing should validate inputs (positive prices, valid dates, reasonable volatility ranges)
- All financial calculations should maintain precision for currency amounts
- Market data should be cached appropriately to respect API rate limits
- Symbol validation should distinguish between different asset types (stocks, ETFs, indices)
- Time zones should be handled correctly for market hours and data timestamps
- It's important to create one tool per file to keep financial calculations separate and maintainable