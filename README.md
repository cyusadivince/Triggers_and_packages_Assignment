# Triggers_and_packages_Assignment




# Database Systems Class Activity

## Team Members
1. **Cyusa Divince** - 27516
2. **Ruhongeka Kevin** -27168



## Project Structure

### Q1 - University System Access Policy


**Description**: Implementation of database access control system with business hours restrictions and audit logging.

**Business Rules**:
- No access on Sabbath (Saturday/Sunday)
- Access only during business hours (Monday-Friday, 8AM-5PM)
- All violation attempts logged for audit compliance


**Key Features**:
- Oracle database triggers for access control
- Autonomous transaction logging
- Real-time violation blocking
- Complete audit trail

### Q2 - HR Employee Management System Package
**Location**: `q2/`

**Description**: PL/SQL package for HR Employee Management System with salary calculations and tax deductions.

**Requirements**:
- Functions to calculate RSSB tax and net salary
- Dynamic procedures for employee operations
- Security context with USER/CURRENT_USER and DEFINER/INVOKER rights
- Bulk operations using loops or cursors



