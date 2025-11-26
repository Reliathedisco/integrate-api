# 🤝 Contributing to Integrate API

First off, **thank you** for considering contributing to Integrate API! It's people like you that make it possible to create high-quality integration templates for the developer community.

## 📋 Table of Contents
- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Submitting an Integration](#submitting-an-integration)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
- [Recognition](#recognition)

---

## Code of Conduct

By participating, you agree to uphold our community standards:
- 🤝 Be respectful and inclusive
- 💡 Provide constructive feedback
- 🎯 Focus on what's best for the community
- 🌟 Show empathy towards other contributors

---

## How Can I Contribute?

### 🪲 Report Bugs
Found something broken? [Open a bug report](https://github.com/Reliathedisco/integrate-api/issues/new?template=bug_report.md) with:
- Clear description
- Steps to reproduce
- Expected vs actual behavior
- Your environment details

### 🧩 Request Integrations
Need a specific API integration? [Submit a request](https://github.com/Reliathedisco/integrate-api/issues/new?template=integration_request.md) explaining:
- Which service/API
- Key features needed
- Your use case

### 🚀 Suggest Features
Have ideas for existing integrations? [Create a feature request](https://github.com/Reliathedisco/integrate-api/issues/new?template=feature_request.md) with:
- Problem it solves
- Proposed solution
- Alternative approaches

### 📝 Improve Documentation
- Fix typos or clarify confusing sections
- Add examples or use cases
- Translate documentation

### 💻 Submit Code
- Fix bugs
- Add new integrations
- Improve existing templates
- Add tests

---

## Development Setup

### Prerequisites
```bash
# Required
- Node.js 18+ 
- npm/yarn/pnpm
- Git
- TypeScript knowledge

# Recommended
- VS Code with ESLint/Prettier
- Postman/Insomnia for API testing
```

### Local Setup
```bash
# 1. Fork the repository
# Click "Fork" button on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/integrate-api.git
cd integrate-api

# 3. Add upstream remote
git remote add upstream https://github.com/Reliathedisco/integrate-api.git

# 4. Install dependencies
npm install

# 5. Create a branch
git checkout -b feature/your-integration-name

# 6. Start development
npm run dev
```

### Testing
```bash
# Run all tests
npm test

# Run specific integration tests
npm test -- stripe

# Run with coverage
npm run test:coverage
```

---

## Submitting an Integration

### Structure Requirements
```typescript
/integrations/your-service/
├── index.ts           // Main export file
├── client.ts          // API client wrapper
├── types.ts           // TypeScript definitions
├── webhooks.ts        // Webhook handlers (if applicable)
├── utils.ts           // Helper functions
├── README.md          // Integration documentation
└── __tests__/         // Test files
    ├── client.test.ts
    └── webhooks.test.ts
```

### Integration Checklist
Your integration must include:

#### ✅ Core Requirements
- [ ] TypeScript types for all public APIs
- [ ] Error handling with meaningful messages
- [ ] Retry logic for network failures
- [ ] Rate limiting (if API has limits)
- [ ] Environment variable validation
- [ ] Comprehensive tests (>80% coverage)

#### 📚 Documentation
- [ ] README with setup instructions
- [ ] Code examples for common use cases
- [ ] API reference
- [ ] Troubleshooting section
- [ ] Migration guide (if replacing existing solution)

#### 🧪 Testing
- [ ] Unit tests for all functions
- [ ] Integration tests with mocked API
- [ ] Webhook signature validation tests
- [ ] Error scenario tests

### Example Integration Template
```typescript
// integrations/your-service/client.ts

import { z } from 'zod';

// Environment validation
const envSchema = z.object({
  YOUR_SERVICE_API_KEY: z.string().min(1),
  YOUR_SERVICE_WEBHOOK_SECRET: z.string().optional(),
});

export class YourServiceClient {
  private apiKey: string;
  
  constructor(config?: { apiKey?: string }) {
    const env = envSchema.parse(process.env);
    this.apiKey = config?.apiKey || env.YOUR_SERVICE_API_KEY;
  }
  
  async makeRequest<T>(
    endpoint: string,
    options?: RequestInit
  ): Promise<T> {
    // Implement with retry logic, error handling, etc.
  }
  
  // ... your methods
}
```

---

## Pull Request Process

### Before Submitting
1. **Update documentation** - Include any new environment variables or setup steps
2. **Add tests** - Ensure coverage doesn't drop
3. **Run linting** - `npm run lint:fix`
4. **Update CHANGELOG** - Add your changes under "Unreleased"
5. **Check bundle size** - Ensure no significant increase

### PR Guidelines
```markdown
## PR Title Format
feat(stripe): add subscription pause functionality
fix(supabase): handle auth refresh errors  
docs(readme): update installation instructions

## PR Description Template
### What does this PR do?
Brief description of changes

### Why is this needed?
Problem it solves or feature it adds

### How to test?
Steps to verify the changes work

### Checklist
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes
- [ ] Follows code style
```

### Review Process
1. **Automated checks** run (tests, linting, build)
2. **Code review** by maintainers (1-3 days)
3. **Feedback addressed** by contributor
4. **Approval & merge** when all checks pass
5. **Release** in next version (bi-weekly)

---

## Style Guidelines

### TypeScript
```typescript
// ✅ Good: Explicit types, clear naming
export interface StripeWebhookEvent {
  id: string;
  type: 'checkout.session.completed' | 'customer.subscription.updated';
  data: Record<string, unknown>;
}

// ❌ Bad: Any types, unclear names
export interface Event {
  id: any;
  t: string;
  d: any;
}
```

### Error Handling
```typescript
// ✅ Good: Specific error with context
throw new IntegrationError('Stripe webhook validation failed', {
  code: 'INVALID_SIGNATURE',
  statusCode: 401,
  details: { receivedSig, expectedSig }
});

// ❌ Bad: Generic error
throw new Error('Invalid webhook');
```

### Documentation
```typescript
/**
 * Creates a Stripe checkout session
 * @param items - Line items for the checkout
 * @param options - Additional session options
 * @returns Checkout session URL
 * @throws {StripeError} If session creation fails
 * @example
 * const url = await createCheckout([
 *   { price: 'price_123', quantity: 1 }
 * ]);
 */
export async function createCheckout(
  items: LineItem[],
  options?: CheckoutOptions
): Promise<string> {
  // Implementation
}
```

### Commit Messages
```bash
# Format: type(scope): description

feat(stripe): add customer portal support
fix(auth): handle token refresh edge case
docs(supabase): add storage examples
test(webhooks): increase coverage to 95%
refactor(types): simplify generic constraints
```

---

## Recognition

### Contributors Wall 🌟
All contributors are recognized in our:
- [README](README.md#contributors) with avatar
- [CONTRIBUTORS](CONTRIBUTORS.md) file with details
- Release notes with contribution mention
- Social media shoutouts for significant contributions

### Contributor Levels
- 🥉 **Bronze**: First PR merged
- 🥈 **Silver**: 3+ PRs merged
- 🥇 **Gold**: 10+ PRs or major integration
- 💎 **Diamond**: Core maintainer

### Perks
- Early access to new features
- Priority issue/PR reviews
- Invitation to contributor Discord
- Potential for maintainer status

---

## Questions?

- 💬 [Start a discussion](https://github.com/Reliathedisco/integrate-api/discussions)
- 🐦 Tweet us [@integrateapi](https://twitter.com/integrateapi)
- 📧 Email: contribute@integrateapi.io

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for making Integrate API better!** 🚀

*Happy coding!*
