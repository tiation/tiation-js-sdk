# Tiation JavaScript SDK

<div align="center">
  <img src="https://via.placeholder.com/800x200/1a1a2e/16213e?text=Tiation+JavaScript+SDK" alt="Tiation JavaScript SDK Banner" />
  
  <h3>Official JavaScript SDK for Tiation APIs</h3>
  
  [![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/tiation/tiation-js-sdk)
  [![JavaScript](https://img.shields.io/badge/javascript-ES2020+-brightgreen.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
  [![TypeScript](https://img.shields.io/badge/typescript-4.8+-blue.svg)](https://www.typescriptlang.org)
  [![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
  [![Enterprise](https://img.shields.io/badge/enterprise-ready-purple.svg)](https://github.com/tiation)
</div>

## 🌟 Overview

The Tiation JavaScript SDK provides a comprehensive, enterprise-grade interface for interacting with all Tiation services. Built with modern JavaScript/TypeScript and designed for both browser and Node.js environments, it offers seamless integration with your web applications.

## ✨ Features

- **🚀 Universal Support**: Works in browser and Node.js environments
- **🔒 Enterprise Security**: Built-in authentication and rate limiting
- **📊 Real-time Analytics**: Live metrics and business intelligence
- **🔄 Promise-based**: Modern async/await support with full TypeScript types
- **🛡️ Type Safety**: Complete TypeScript definitions included
- **📚 Rich Documentation**: Comprehensive docs with examples
- **⚡ Lightweight**: Minimal bundle size with tree-shaking support

## 📦 Installation

```bash
# npm
npm install @tiation/sdk

# yarn
yarn add @tiation/sdk

# pnpm
pnpm add @tiation/sdk
```

## 🚀 Quick Start

### JavaScript (ES6+)
```javascript
import { TiationClient } from '@tiation/sdk';

// Initialize client
const client = new TiationClient('your_api_key');

// Get business analytics
const analytics = await client.analytics.getMetrics();
console.log(`Total revenue: $${analytics.revenue}`);

// Create automation workflow
const workflow = await client.automation.createWorkflow({
  name: 'Customer Onboarding',
  trigger: 'user_signup',
  actions: ['send_welcome_email', 'create_profile']
});

console.log(`Workflow created: ${workflow.id}`);
```

### TypeScript
```typescript
import { TiationClient, Analytics, Workflow } from '@tiation/sdk';

// Initialize client with full type support
const client = new TiationClient('your_api_key');

// Get business analytics with type safety
const analytics: Analytics = await client.analytics.getMetrics();
console.log(`Total revenue: $${analytics.revenue}`);

// Create automation workflow with typed parameters
const workflow: Workflow = await client.automation.createWorkflow({
  name: 'Customer Onboarding',
  trigger: 'user_signup',
  actions: ['send_welcome_email', 'create_profile']
});
```

## 📚 Documentation

### Authentication

```javascript
import { TiationClient } from '@tiation/sdk';

// API Key authentication
const client = new TiationClient('your_api_key');

// OAuth2 authentication
const client = new TiationClient({
  clientId: 'your_client_id',
  clientSecret: 'your_client_secret',
  oauthToken: 'your_oauth_token'
});
```

### Core Services

#### Analytics & Metrics
```javascript
// Get business metrics
const metrics = await client.analytics.getMetrics({
  startDate: '2024-01-01',
  endDate: '2024-12-31'
});

// Real-time dashboard data
const dashboard = await client.analytics.getDashboard();

// Subscribe to real-time updates
client.analytics.subscribe('metrics', (data) => {
  console.log('New metrics:', data);
});
```

#### Automation Workflows
```javascript
// List workflows
const workflows = await client.automation.listWorkflows();

// Execute workflow
const result = await client.automation.executeWorkflow({
  workflowId: 'workflow_123',
  parameters: { userId: 'user_456' }
});

// Monitor workflow status
const status = await client.automation.getWorkflowStatus(result.id);
```

#### Content Management
```javascript
// Create content
const content = await client.cms.createContent({
  title: 'New Product Launch',
  body: 'Exciting new features available now!',
  category: 'announcements'
});

// Update content
await client.cms.updateContent(content.id, {
  status: 'published'
});

// Search content
const results = await client.cms.searchContent({
  query: 'product launch',
  category: 'announcements'
});
```

### Advanced Features

#### Real-time Subscriptions
```javascript
// Subscribe to real-time events
client.subscribe('user.created', (event) => {
  console.log('New user:', event.data);
});

// Multiple subscriptions
client.subscribe(['order.created', 'payment.completed'], (event) => {
  console.log('Business event:', event.type, event.data);
});

// Unsubscribe
client.unsubscribe('user.created');
```

#### Error Handling
```javascript
try {
  const analytics = await client.analytics.getMetrics();
} catch (error) {
  if (error.type === 'RateLimitError') {
    console.log(`Rate limit exceeded, retry after: ${error.retryAfter}s`);
  } else if (error.type === 'ApiError') {
    console.log(`API error: ${error.message} (code: ${error.code})`);
  } else {
    console.log(`SDK error: ${error.message}`);
  }
}
```

## 🔧 Configuration

### Environment Variables
```bash
TIATION_API_KEY=your_api_key
TIATION_BASE_URL=https://api.tiation.com
TIATION_TIMEOUT=30000
```

### Configuration Object
```javascript
const client = new TiationClient({
  apiKey: 'your_api_key',
  baseUrl: 'https://api.tiation.com',
  timeout: 30000,
  maxRetries: 3,
  retryDelay: 1000
});
```

## 🌐 Browser Support

### Modern Browsers
```html
<script type="module">
  import { TiationClient } from 'https://cdn.jsdelivr.net/npm/@tiation/sdk/dist/tiation.esm.js';
  
  const client = new TiationClient('your_api_key');
  // Use client...
</script>
```

### Legacy Browser Support
```html
<script src="https://cdn.jsdelivr.net/npm/@tiation/sdk/dist/tiation.umd.js"></script>
<script>
  const client = new TiationSDK.TiationClient('your_api_key');
  // Use client...
</script>
```

## 🏢 Enterprise Features

### Batch Operations
```javascript
// Batch create content
const contents = [
  { title: 'Article 1', body: 'Content 1' },
  { title: 'Article 2', body: 'Content 2' }
];

const results = await client.cms.batchCreate(contents);

// Batch analytics
const metrics = await client.analytics.batchMetrics([
  { metric: 'revenue', period: 'monthly' },
  { metric: 'users', period: 'daily' }
]);
```

### Webhook Integration
```javascript
// Express.js webhook handler
app.post('/webhooks/tiation', (req, res) => {
  const event = client.webhooks.parseEvent(req.body, req.headers);
  
  switch (event.type) {
    case 'user.created':
      console.log('New user:', event.data);
      // Trigger welcome workflow
      client.automation.executeWorkflow({
        workflowId: 'welcome_workflow',
        parameters: { userId: event.data.id }
      });
      break;
  }
  
  res.json({ received: true });
});
```

### React Integration
```jsx
import { useTiation } from '@tiation/sdk/react';

function Dashboard() {
  const { analytics, loading, error } = useTiation({
    apiKey: 'your_api_key',
    autoFetch: ['analytics.getMetrics']
  });
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return (
    <div>
      <h1>Revenue: ${analytics.revenue}</h1>
      <p>Users: {analytics.users}</p>
    </div>
  );
}
```

## 🧪 Testing

```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage

# Run specific test
npm test -- --testNamePattern="analytics"
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
# Clone repository
git clone https://github.com/tiation/tiation-js-sdk.git
cd tiation-js-sdk

# Install dependencies
npm install

# Build the project
npm run build

# Run tests
npm test
```

## 📞 Support

- **Documentation**: [JavaScript SDK Docs](https://docs.tiation.com/js-sdk)
- **API Reference**: [API Documentation](https://api.tiation.com/docs)
- **Issues**: [GitHub Issues](https://github.com/tiation/tiation-js-sdk/issues)
- **Enterprise Support**: [tiatheone@protonmail.com](mailto:tiatheone@protonmail.com)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <p>Built with ❤️ by <a href="https://github.com/tiation">Tiation</a></p>
  <p>Modern JavaScript SDK for web and Node.js applications</p>
</div>
