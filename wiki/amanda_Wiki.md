# SigmaOS-amanda Component Wiki

## Overview
SigmaOS-amanda provides Amanda backup and disk array support for the SigmaOS operating system. It demonstrates the backup subsystem and disk array management within the SigmaOS ecosystem, following the principles of clear abstraction and deterministic backup initialization.

## Principles
- Single Responsibility
- Backup Abstraction
- Fail-Fast on Backup Initialization Errors
- Deterministic Backup Setup
- Clear Abstraction Over Backup APIs
- Composition over Inheritance for backup extensions

## Architecture
SigmaOS-amanda follows a backup pattern:
- **Backup Core**: Provides backup management, disk array support, and backup scheduling
- **Array Management**: Supports disk array creation, disk array configuration, and disk array monitoring
- **Backup Scheduling**: Supports backup jobs, backup rotation, and backup retention policies
- **Error Handling**: Fail-fast on invalid backup configurations or unsupported backup types

## API
The component provides the following public APIs:
- `backup::array::create(name)` - Create a disk array by given name
- `backup::schedule::add(backup)` - Add a backup job with given schedule
- `backup::status::array()` - Get backup array status and backup jobs
- `backup::retention::policy(policy)` - Set backup retention policy
- Error types for backup failure scenarios or unsupported backup types

## Test Structure (Arrange-Act-ASSERT)
All tests follow the AAA pattern:
1. **Arrange**: Set up test environment with specific backup configuration
2. **Act**: Execute the code under test (array creation, backup scheduling)
3. **Assert**: Verify the expected backup results

Example:
```rust
#[test]
fn test_backup_array_aaa() {
    // Arrange
    let array_name = "backup-array-1";
    
    // Act
    let result = backup::array::create(array_name);
    
    // Assert
    assert!(result.is_ok());
    let created = result.unwrap();
    assert!(created.is_valid());
}
```

## Development
- Follows Rust best practices with `#![forbid(unsafe_code)]`
- Backup initialization is best-effort; gracefully degrades on unsupported configurations
- Comprehensive error types for all backup failure scenarios
- Unit tests provided for array creation and backup scheduling
- Integration tests for full backup system with actual disk array integration

## TODO
- Add support for additional backup types (incremental, differential, full backup)
- Expand array management capabilities (array resizing, array migration, array recovery)
- Add scheduling features (backup frequency, backup rotation, backup notifications)
- Create integration tests with actual disk array systems and backup integration
- Implement backup persistence and array state management