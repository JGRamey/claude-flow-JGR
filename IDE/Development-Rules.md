🎯 Core Development Mandate

**All development of the Claude Flow IDE MUST use Claude Flow's agent system for implementation while building an IDE that seamlessly integrates with Claude Flow for end users.**

These rules are **NON-NEGOTIABLE** and apply to every line of code, every feature, and every decision made in this project.

---

## 📋 Rule 1: Claude Flow-Driven Development (MANDATORY)

### 1.1 Use Claude Flow Agents for ALL Development

```bash
# NEVER write code manually when Claude Flow agents can do it
# ALWAYS use appropriate Claude Flow agents for each task

# ✅ CORRECT: Using Claude Flow agents
npx claude-flow@alpha swarm "create MonacoEditor component with tests" --agents tester,coder
npx claude-flow@alpha sparc tdd "implement WebSocket service"

# ❌ WRONG: Manual coding without Claude Flow
vim src/components/MonacoEditor.tsx  # NO! Use agents instead
```

### 1.2 Agent Selection Matrix

| Task Type | Required Agents | Command Example |
|-----------|----------------|-----------------|
| **Component Creation** | `frontend-dev`, `tester`, `reviewer` | `swarm "create FileExplorer component"` |
| **Service Implementation** | `backend-dev`, `tester`, `architect` | `swarm "implement ClaudeFlowService"` |
| **Test Writing** | `tester`, `sparc-tdd` | `sparc tdd "test WebSocket communication"` |
| **Architecture Design** | `system-architect`, `planner` | `hive-mind spawn "design module structure"` |
| **Code Review** | `reviewer`, `security-analyst` | `swarm "review authentication module"` |
| **Documentation** | `documentor`, `api-docs` | `swarm "document API endpoints"` |

### 1.3 Development Workflow Using Claude Flow

```bash
# 1. PLANNING PHASE - Use hive-mind for architecture
npx claude-flow@alpha hive-mind spawn "plan IDE module structure" \
  --agents architect,planner,frontend-dev,backend-dev

# 2. IMPLEMENTATION PHASE - Use swarm for coding
npx claude-flow@alpha swarm "implement [feature]" \
  --topology hierarchical \
  --continue-session

# 3. TESTING PHASE - Use SPARC TDD
npx claude-flow@alpha sparc tdd "[feature] test suite"

# 4. REVIEW PHASE - Use specialized agents
npx claude-flow@alpha swarm "review and optimize [feature]" \
  --agents reviewer,optimizer,security-analyst

# 5. DOCUMENTATION PHASE
npx claude-flow@alpha swarm "document [feature]" \
  --agents documentor,api-docs
```

---

## 📋 Rule 2: Test-Driven Development with SPARC (MANDATORY)

### 2.1 SPARC TDD Workflow

**EVERY feature MUST follow the SPARC methodology:**

```
Specification → Pseudocode → Architecture → Refinement → Code
```

### 2.2 Test-First Implementation

```bash
# STEP 1: Write specifications and tests FIRST
npx claude-flow@alpha sparc spec "define [feature] requirements"
npx claude-flow@alpha sparc tdd "create [feature] tests"

# STEP 2: Only then implement
npx claude-flow@alpha sparc code "implement [feature]"

# NEVER skip directly to code
```

### 2.3 Test Coverage Requirements

```typescript
// Minimum coverage thresholds (enforced by CI/CD)
{
  "coverage": {
    "global": 80,         // Minimum 80% overall
    "critical": {         // 100% for critical paths
      "claudeFlowService": 100,
      "webSocketBridge": 100,
      "agentCoordination": 100,
      "fileOperations": 100,
      "stateManagement": 100
    }
  }
}
```

### 2.4 Test File Creation Rules

```bash
# Test files MUST be created BEFORE implementation files
# Use Claude Flow to generate test scaffolding

npx claude-flow@alpha swarm "create test suite for [Component]" \
  --template tdd \
  --coverage-target 100

# The swarm will create:
# 1. src/features/[feature]/__tests__/[Component].test.tsx
# 2. Test fixtures and mocks
# 3. Integration test scenarios
# 4. Edge case coverage
```

---

## 📋 Rule 3: Claude Flow Integration Requirements

### 3.1 Dual-Mode Development

The IDE has two Claude Flow integration points that MUST be maintained:

```typescript
// 1. DEVELOPMENT MODE: Using Claude Flow to BUILD the IDE
interface DevelopmentMode {
  agents: ['coder', 'tester', 'reviewer', 'architect'];
  workflow: 'hive-mind' | 'swarm';
  memory: '.swarm/memory.db';  // Development memory
}

// 2. RUNTIME MODE: IDE using Claude Flow for end users
interface RuntimeMode {
  cli: 'npx claude-flow@alpha';
  communication: 'WebSocket';
  agents: '54+ available agents';
  tools: '87 MCP tools';
  memory: '~/.claude-flow/memory.db';  // User memory
}
```

### 3.2 WebSocket Bridge Specification

```typescript
// MANDATORY: All Claude Flow communication through WebSocket
class ClaudeFlowBridge {
  // Required endpoints
  readonly endpoints = {
    '/agent/spawn': 'Spawn new agents',
    '/agent/status': 'Monitor agent activity',
    '/swarm/execute': 'Execute swarm commands',
    '/memory/query': 'Query memory system',
    '/tools/execute': 'Execute MCP tools'
  };
  
  // Required error handling
  readonly errorHandlers = {
    'AGENT_TIMEOUT': 'Retry with fallback',
    'MEMORY_FULL': 'Compress and continue',
    'TOOL_FAILURE': 'Log and notify user'
  };
}
```

### 3.3 Memory System Integration

```bash
# Development memory (building the IDE)
.swarm/
  └── memory.db         # Development decisions and context

# Runtime memory (IDE in use)
~/.claude-flow/
  └── memory.db         # User's project memory

# MUST maintain separation between these two systems
```

---

## 📋 Rule 4: Module Architecture Rules

### 4.1 Module Independence

```typescript
// EVERY module MUST be self-contained
interface ModuleStructure {
  required: {
    'index.ts': 'Public API exports only',
    '__tests__/': 'Test files (created FIRST)',
    'types.ts': 'TypeScript interfaces',
    'README.md': 'Module documentation'
  };
  optional: {
    'components/': 'React components',
    'services/': 'Business logic',
    'hooks/': 'Custom React hooks',
    'utils/': 'Helper functions'
  };
}
```

### 4.2 Inter-Module Communication

```typescript
// Modules MUST communicate through:
// 1. Event emitters
// 2. Zustand stores
// 3. WebSocket messages
// NEVER through direct imports

// ✅ CORRECT
import { useClaudeFlowStore } from '@/store';
const { executeCommand } = useClaudeFlowStore();

// ❌ WRONG
import { ClaudeFlowService } from '../claude-flow/service';
```

### 4.3 Feature Flags for Progressive Enhancement

```typescript
// All features MUST be feature-flagged
const FEATURES = {
  'MONACO_EDITOR': true,      // Core feature
  'AGENT_MONITOR': true,       // Core feature
  'HIVE_MIND_VIZ': false,     // Progressive enhancement
  'MCP_TOOLS_UI': false,      // Progressive enhancement
  'COLLAB_MODE': false        // Future feature
};

// Use Claude Flow to manage feature rollout
npx claude-flow@alpha swarm "enable feature flag MCP_TOOLS_UI"
```

---

## 📋 Rule 5: Quality Gates & CI/CD

### 5.1 Pre-Commit Hooks (MANDATORY)

```json
{
  "husky": {
    "hooks": {
      "pre-commit": [
        "npm run test:changed",      // Test changed files
        "npm run lint:fix",          // Auto-fix linting
        "npm run type-check",        // TypeScript validation
        "npm run test:coverage:check" // Coverage threshold
      ]
    }
  }
}
```

### 5.2 Claude Flow Review Process

```bash
# EVERY PR must go through Claude Flow review
npx claude-flow@alpha swarm "review PR #[number]" \
  --agents reviewer,security-analyst,performance-analyst \
  --output review-report.md

# Merge ONLY after Claude Flow approval
```

### 5.3 Deployment Pipeline

```yaml
# Claude Flow agents handle deployment
deploy:
  steps:
    - name: "Claude Flow Build Check"
      run: npx claude-flow@alpha swarm "verify build readiness"
    
    - name: "Claude Flow Test Suite"
      run: npx claude-flow@alpha sparc test "run full test suite"
    
    - name: "Claude Flow Security Scan"
      run: npx claude-flow@alpha swarm "security audit" --agents security-analyst
    
    - name: "Claude Flow Deploy"
      run: npx claude-flow@alpha swarm "deploy to production" --agents devops-engineer
```

---

## 📋 Rule 6: Documentation Requirements

### 6.1 Self-Documenting Code via Claude Flow

```bash
# Use Claude Flow to maintain documentation
npx claude-flow@alpha swarm "document [module]" \
  --style comprehensive \
  --include-examples \
  --update-readme

# Documentation must include:
# - Purpose and responsibilities
# - API reference
# - Usage examples
# - Integration points
# - Testing instructions
```

### 6.2 Inline Documentation Standards

```typescript
/**
 * EVERY public API MUST have JSDoc comments
 * Generated by: claude-flow@alpha swarm "document API"
 * 
 * @description Executes Claude Flow command through WebSocket
 * @param {string} command - The Claude Flow command to execute
 * @param {AgentType[]} agents - Array of agents to use
 * @returns {Promise<CommandResult>} - Execution result with metadata
 * @throws {ClaudeFlowError} - If command execution fails
 * 
 * @example
 * const result = await executeCommand('swarm "build component"', ['coder', 'tester']);
 */
```

---

## 📋 Rule 7: Performance & Monitoring

### 7.1 Performance Budgets

```typescript
// ENFORCED performance metrics
const PERFORMANCE_BUDGETS = {
  'IDE_LOAD_TIME': 2000,        // 2 seconds max
  'AGENT_SPAWN_TIME': 340,      // 340ms max
  'FILE_OPERATION': 50,         // 50ms max
  'WEBSOCKET_LATENCY': 10,      // 10ms max
  'MEMORY_QUERY': 100,          // 100ms max
  'BUILD_TIME': 30000,          // 30 seconds max
  'TEST_SUITE': 60000           // 60 seconds max
};

// Use Claude Flow to monitor
npx claude-flow@alpha performance monitor --thresholds performance.json
```

### 7.2 Real-Time Monitoring

```bash
# Claude Flow agents monitor the IDE during development
npx claude-flow@alpha swarm "monitor performance metrics" \
  --agents performance-analyst \
  --real-time \
  --alert-threshold 80
```

---

## 📋 Rule 8: Error Handling & Recovery

### 8.1 Graceful Degradation

```typescript
// EVERY Claude Flow integration MUST have fallbacks
class ClaudeFlowIntegration {
  async executeWithFallback(command: string) {
    try {
      // Primary: Use Claude Flow CLI
      return await this.claudeFlowCLI.execute(command);
    } catch (error) {
      // Fallback 1: Try alternative agent
      try {
        return await this.tryAlternativeAgent(command);
      } catch {
        // Fallback 2: Queue for retry
        return await this.queueForRetry(command);
      }
    }
  }
}
```

### 8.2 Error Recovery via Claude Flow

```bash
# Use Claude Flow to diagnose and fix errors
npx claude-flow@alpha swarm "diagnose error: [error message]" \
  --agents debugger,reviewer \
  --suggest-fix \
  --auto-implement
```

---

## 📋 Rule 9: Security Requirements

### 9.1 Security-First Development

```bash
# EVERY feature must pass security review
npx claude-flow@alpha swarm "security audit [feature]" \
  --agents security-analyst \
  --owasp-checklist \
  --penetration-test

# Security checks include:
# - Input validation
# - XSS prevention
# - CSRF protection
# - Secure WebSocket communication
# - File system access controls
```

### 9.2 Secure Claude Flow Integration

```typescript
// Sandbox all Claude Flow operations
const CLAUDE_FLOW_SANDBOX = {
  allowedCommands: ['swarm', 'hive-mind', 'sparc'],
  blockedOperations: ['rm', 'sudo', 'eval'],
  maxMemoryUsage: '1GB',
  timeout: 30000,
  rateLimiting: {
    maxRequests: 100,
    window: '1m'
  }
};
```

---

## 📋 Rule 10: Development Environment

### 10.1 Standardized Development Setup

```bash
# EVERYONE must use the same Claude Flow configuration
# Setup script using Claude Flow
npx claude-flow@alpha swarm "setup development environment" \
  --template ide-development \
  --install-deps \
  --configure-vscode \
  --setup-git-hooks
```

### 10.2 Required VS Code Extensions

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "vitest.explorer",
    "github.copilot",
    "anthropic.claude-code",
    "ms-vscode.vscode-typescript-next"
  ]
}
```

---

## 🚨 Violations & Enforcement

### Automatic Enforcement

```bash
# CI/CD pipeline blocks merges for violations
- No tests = No merge
- Coverage below 80% = No merge
- No Claude Flow review = No merge
- Performance regression = No merge
- Security vulnerabilities = No merge
```

### Manual Review Requirements

1. **Architecture changes** must be approved by:
   - System architect agent
   - Two human reviewers
   - Performance analyst agent

2. **Claude Flow integration changes** must be:
   - Tested in isolation
   - Backward compatible
   - Documented with migration guide

---

## 📊 Success Metrics

### Development Velocity
- **Features per sprint**: Track via Claude Flow memory
- **Test coverage trend**: Must increase or maintain
- **Bug escape rate**: < 1% to production
- **Claude Flow agent efficiency**: > 80% task success

### Code Quality
- **Type coverage**: 100% required
- **Documentation coverage**: 100% for public APIs
- **Cyclomatic complexity**: < 10 per function
- **Duplication**: < 3% across codebase

---

## 🏁 Golden Rules Summary

1. **Claude Flow First**: Use Claude Flow agents for ALL development tasks
2. **Test Before Code**: Write tests BEFORE implementation (SPARC TDD)
3. **WebSocket Only**: All Claude Flow communication via WebSocket
4. **Module Independence**: No direct inter-module imports
5. **Feature Flags**: Every feature must be toggleable
6. **80% Coverage Minimum**: 100% for critical paths
7. **Performance Budgets**: Enforce and monitor continuously
8. **Security Reviews**: Every feature audited by security-analyst
9. **Documentation Complete**: Generate with documentor agent
10. **Continuous Integration**: Claude Flow agents handle CI/CD

---

## 📝 Amendment Process

These rules can only be amended through:

1. **Proposal via Claude Flow**:
   ```bash
   npx claude-flow@alpha swarm "propose rule change: [description]" \
     --agents architect,planner,reviewer
   ```

2. **Team consensus** (>75% approval)
3. **Performance impact analysis**
4. **Security impact review**
5. **Documentation update**

---

**Remember**: These rules exist to ensure we build a world-class IDE using Claude Flow's power while creating an IDE that seamlessly integrates with Claude Flow for end users. Every decision should enhance both the development process AND the final user experience.

**USE CLAUDE FLOW. TEST FIRST. BUILD MODULAR. SHIP QUALITY.**

---

**Document Version**: 2.0.0  
**Last Updated**: September 2025  
**Enforcement**: MANDATORY  
**Review Cycle**: Sprint Retrospectives  
**Owner**: Lead Architect & Claude Flow Integration Team



🚀 Key Commands Structure:

bash

# Planning with hive-mind
npx claude-flow@alpha hive-mind spawn "plan feature"

# Implementation with swarm
npx claude-flow@alpha swarm "implement feature"

# Testing with SPARC
npx claude-flow@alpha sparc tdd "test feature"

# Review with specialized agents
npx claude-flow@alpha swarm "review feature" --agents reviewer,security-analyst
