---
applyTo: "**/*test*/**,**/*.test.*,**/*Test.*,**/*_test.*,**/test_*"
---

# Testing Best Practices

## Fundamental Principle: Tests Verify, Not Implement

Tests should **verify behavior**, not **re-implement logic**. If your test contains parsing, transformation, or business logic that mirrors the implementation, it is likely testing itself rather than the actual code.

## Anti-Patterns to Avoid

### 1. Do NOT Copy Implementation Logic into Tests

**Bad: Test re-implements parsing logic**
```typescript
test('parses scenario correctly', () => {
    const content = 'scenario: Test';
    // BAD: This is copying the parser implementation
    const match = content.match(/^scenario:\s*(.+)/);
    assert.ok(match);
    assert.strictEqual(match[1], 'Test');
});
```

**Good: Test verifies provider behavior**
```typescript
test('scenario is recognized as symbol', async () => {
    const symbols = await vscode.commands.executeCommand(
        'vscode.executeDocumentSymbolProvider',
        doc.uri
    );
    const hasScenario = symbols.some(s => s.name.includes('scenario:'));
    assert.ok(hasScenario);
});
```

### 2. Do NOT Parse Fixture Files in Tests

**Bad: Test parses fixture to validate parsing**
```typescript
test('operationIds are parsed', () => {
    const yaml = fs.readFileSync('petstore.yaml', 'utf-8');
    // BAD: Re-implementing YAML parsing in test
    const match = yaml.match(/operationId:\s*(\w+)/g);
    assert.strictEqual(match.length, 5);
});
```

**Good: Test uses actual provider**
```typescript
test('operationIds are available for completion', async () => {
    const completions = await vscode.commands.executeCommand(
        'vscode.executeCompletionItemProvider',
        doc.uri,
        position
    );
    assert.ok(completions.items.length > 0);
});
```

### 3. Do NOT Duplicate Validation Logic

If the implementation validates input, the test should provide valid/invalid inputs and check the result—not repeat the validation regex.

## Best Practices

### Use Real APIs and Commands

- **VS Code extensions**: Use `vscode.commands.executeCommand()` with provider commands
- **REST APIs**: Call actual endpoints, not mock implementations
- **Libraries**: Use public APIs, not internal parsing functions

### Test Behavior, Not Internals

Ask: "What should happen when a user does X?" not "Does my regex match the expected pattern?"

### Use Fixture Files Without Parsing Them

Fixture files provide realistic test data. Read them, pass them to providers, and verify the output—don't parse them to validate parsing.

### Prefer Integration Over Unit When Logic Is Complex

If testing a parser, symbol provider, or formatter:
- Create realistic fixtures
- Pass fixtures through the actual code path
- Verify expected outputs

### Tests Should Fail When Implementation Breaks

If you change the implementation and tests still pass, the tests may be testing themselves. Good tests fail when the code they test is broken.

## Examples by Language

### TypeScript/JavaScript (VS Code Extension)
```typescript
// Use VS Code command APIs
const symbols = await vscode.commands.executeCommand('vscode.executeDocumentSymbolProvider', uri);
const definitions = await vscode.commands.executeCommand('vscode.executeDefinitionProvider', uri, position);
```

### Kotlin/Java (IntelliJ Plugin)
```kotlin
// Use test fixtures and runInEditorWithFixture
myFixture.configureByText("test.scenario", content)
val symbols = myFixture.findAllElementsInDocument()
```

### Python
```python
# Call actual functions, verify outputs
result = parse_scenario(content)
assert 'feature' in result
```

## Summary

| Do | Don't |
|----|-------|
| Call providers/APIs | Re-implement parsing |
| Verify outputs | Duplicate logic |
| Use fixtures as input | Parse fixtures to validate |
| Test user-visible behavior | Test internal implementation details |
| Let tests fail on regression | Write tests that always pass |
