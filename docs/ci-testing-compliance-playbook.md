# CI Testing & Compliance Playbook for Doctrine Enforcement

## Overview

This playbook provides comprehensive procedures for testing CI pipeline functionality and ensuring doctrine compliance within the Circuittelligence development framework. It establishes standardized testing protocols, verification procedures, and troubleshooting guidelines to maintain operational excellence and security standards.

## 1. Pull Request Procedures Using Templates & Checklists

### 1.1 Standard Pull Request Creation Protocol

#### Prerequisites Verification
- [ ] Confirm branch naming follows convention: `feature/`, `bugfix/`, `hotfix/`, or `chore/`
- [ ] Verify all local commits follow conventional commit format
- [ ] Ensure working directory is clean with no uncommitted changes
- [ ] Confirm target branch is correct (typically `develop` for features, `main` for hotfixes)

#### Template Utilization Process
1. **Initialize Pull Request**
   - Navigate to repository and select "New Pull Request"
   - Verify correct base and compare branches
   - Template auto-population should occur automatically

2. **Complete Required Sections**
   - **Summary**: Provide clear, concise description of changes
   - **Type of Change**: Select appropriate classification
   - **Testing**: Document all testing performed
   - **Checklist Completion**: Mark all applicable items
   - **Breaking Changes**: Document any backwards compatibility impacts
   - **Documentation**: Confirm updates to relevant documentation

3. **Security & Compliance Declaration**
   - Review and acknowledge security implications
   - Confirm compliance with coding standards
   - Validate data handling procedures if applicable

### 1.2 Checklist Verification Protocol

#### Pre-Submission Checklist
- [ ] Code follows established style guidelines
- [ ] All tests pass locally
- [ ] Documentation updated for public API changes
- [ ] Security review completed for sensitive changes
- [ ] Performance impact assessed
- [ ] Backwards compatibility maintained or properly documented

#### Post-Submission Validation
- [ ] CI pipeline triggered successfully
- [ ] All automated checks passing
- [ ] Proper reviewers assigned
- [ ] Labels applied correctly
- [ ] Milestone associated if applicable

## 2. Auto-Assignment and Notification Verification

### 2.1 Assignment Verification Protocol

#### Automated Assignment Checks
1. **Code Owner Assignment**
   - Verify CODEOWNERS file triggers appropriate reviewer assignment
   - Confirm team leads automatically assigned for architecture changes
   - Validate security team inclusion for sensitive file modifications

2. **Area-Specific Assignment Rules**
   ```
   Frontend Changes → Frontend Team Lead + UI/UX Reviewer
   Backend API → Backend Team Lead + Security Reviewer
   Infrastructure → DevOps Team + Security Team
   Documentation → Technical Writer + Subject Matter Expert
   ```

3. **Escalation Path Verification**
   - Test assignment fallback when primary reviewers unavailable
   - Confirm management notification for high-priority changes
   - Validate cross-team assignment for multi-area changes

### 2.2 Notification Testing Procedures

#### Notification Verification Matrix
| Event | Expected Recipients | Notification Method | Verification Steps |
|-------|-------------------|-------------------|------------------|
| PR Created | Assignees, Watchers | Email + In-app | Check recipient lists, verify delivery |
| Review Requested | Specific Reviewers | Email + In-app | Confirm reviewer notification receipt |
| Changes Requested | PR Author | Email + In-app | Validate author notification |
| PR Approved | Author, Assignees | Email + In-app | Check approval notifications |
| PR Merged | All Participants | Email + In-app | Verify merge notifications |
| CI Failure | Author, Reviewers | Email + In-app + Slack | Multi-channel verification |

#### Testing Notification Delivery
1. **Create Test Pull Request**
   - Use dedicated test branch
   - Include changes that trigger various assignment rules
   - Monitor notification delivery across all channels

2. **Verify Notification Content**
   - Confirm notifications contain relevant context
   - Validate links direct to correct PR sections
   - Check notification timing and frequency

## 3. Security Check Triggers and Artifact Review

### 3.1 Security Scan Trigger Verification

#### Automated Security Triggers
1. **Secret Scanning (Gitleaks)**
   ```bash
   # Test secret detection
   echo "api_key = 'test_123456789'" > test_secrets.txt
   git add test_secrets.txt
   git commit -m "test: trigger secret scan"
   # Verify Gitleaks detects and blocks
   ```

2. **Dependency Vulnerability Scanning**
   - Add known vulnerable dependency to test detection
   - Verify scan executes on package.json/requirements.txt changes
   - Confirm high-severity findings block PR merge

3. **Code Quality Security Rules**
   - Test injection vulnerability patterns
   - Verify authentication bypass detection
   - Confirm cryptographic weakness identification

### 3.2 Security Artifact Review Protocol

#### Artifact Collection Verification
1. **SARIF Report Generation**
   - Confirm SARIF files uploaded to GitHub Security tab
   - Verify report completeness and accuracy
   - Check integration with GitHub Advanced Security

2. **Scan Report Accessibility**
   ```
   Artifacts to Verify:
   - gitleaks-scan-reports/
     ├── gitleaks-report.sarif
     ├── gitleaks-report.json
     └── scan-summary.md
   - dependency-scan-reports/
     ├── vulnerability-report.json
     ├── dependency-tree.txt
     └── remediation-suggestions.md
   ```

3. **Report Review Process**
   - Download and examine each artifact type
   - Verify report timestamps and scan coverage
   - Confirm findings categorization (High/Medium/Low)
   - Validate false positive marking capability

### 3.3 Security Gate Enforcement

#### Critical Security Blocking Conditions
- High-severity secrets detected
- Critical vulnerability dependencies
- Security policy violations
- Insufficient test coverage for security-sensitive code

#### Security Override Procedures
- Emergency hotfix bypass (requires C-level approval)
- False positive acknowledgment process
- Risk acceptance documentation requirements

## 4. Compliance Check Enforcement Scenarios

### 4.1 Standard Compliance Enforcement

#### Mandatory Compliance Checks
1. **Code Quality Gates**
   - Minimum test coverage: 80%
   - Code complexity thresholds
   - Style guide adherence
   - Documentation completeness

2. **Security Compliance Verification**
   ```yaml
   Required Checks:
   - secrets-scan: PASS
   - dependency-audit: PASS
   - license-compliance: PASS
   - security-policy-adherence: PASS
   ```

3. **Process Compliance Validation**
   - PR template completion: 100%
   - Required approvals: Met
   - Branch protection rules: Enforced
   - Conventional commits: Validated

### 4.2 Override and Exemption Procedures

#### Emergency Override Protocol
1. **Justification Documentation**
   ```markdown
   Override Request:
   - Issue: [Critical production outage]
   - Risk Assessment: [Low/Medium/High]
   - Business Impact: [Quantified impact]
   - Remediation Plan: [Post-merge actions]
   - Approver: [Name and role]
   ```

2. **Override Implementation**
   - Apply `emergency-override` label
   - Document override in PR description
   - Set follow-up remediation tasks
   - Notify security team of bypass

#### Exemption Categories
1. **Technical Exemptions**
   - Legacy code maintenance (temporary)
   - Third-party integration constraints
   - Performance optimization trade-offs

2. **Business Exemptions**
   - Regulatory compliance deadlines
   - Critical customer commitments
   - Market opportunity windows

#### Exemption Request Process
```
1. Submit exemption request via GitHub issue
2. Technical review by architecture team
3. Security assessment if applicable
4. Business justification validation
5. Time-bound approval with review date
6. Documentation in compliance register
```

## 5. Review and Troubleshooting Best Practices

### 5.1 Review Process Optimization

#### Effective Review Strategies
1. **Structured Review Approach**
   ```
   Review Order:
   1. Architecture and design patterns
   2. Security implications
   3. Business logic correctness
   4. Code quality and maintainability
   5. Testing adequacy
   6. Documentation completeness
   ```

2. **Review Quality Metrics**
   - Average review time: < 4 hours for standard PRs
   - Review thoroughness: Minimum 2 approvals
   - Feedback quality: Constructive and actionable
   - Follow-up completion: 100% of requested changes

#### Review Checklist for Reviewers
- [ ] Understand the business context and requirements
- [ ] Review automated check results before manual review
- [ ] Test critical paths locally if necessary
- [ ] Verify security implications of changes
- [ ] Check for potential performance impacts
- [ ] Ensure adequate test coverage
- [ ] Validate documentation updates
- [ ] Consider backwards compatibility

### 5.2 Common CI Pipeline Issues and Solutions

#### Frequent Pipeline Failures

1. **Build Failures**
   ```bash
   # Diagnosis Steps:
   # 1. Check build logs for specific errors
   # 2. Verify dependency versions
   # 3. Confirm environment configuration
   # 4. Test locally with identical conditions
   
   # Common Solutions:
   - Update package lock files
   - Clear cache and rebuild
   - Fix environment variable configuration
   - Resolve dependency conflicts
   ```

2. **Test Failures**
   ```bash
   # Troubleshooting Process:
   # 1. Identify failing test categories
   # 2. Check for environment-specific issues
   # 3. Verify test data and fixtures
   # 4. Review recent changes affecting tests
   
   # Resolution Strategies:
   - Fix flaky tests with proper mocking
   - Update test data for new requirements
   - Improve test isolation
   - Add missing test dependencies
   ```

3. **Security Scan Issues**
   ```bash
   # Common Security Issues:
   # 1. False positive secret detection
   # 2. New vulnerability in dependencies
   # 3. Compliance rule violations
   
   # Resolution Approach:
   - Review and whitelist false positives
   - Update vulnerable dependencies
   - Document compliance exceptions
   - Implement security fixes
   ```

### 5.3 Pipeline Performance Optimization

#### Performance Monitoring
1. **Pipeline Duration Metrics**
   - Target total pipeline time: < 10 minutes
   - Build stage: < 3 minutes
   - Test stage: < 5 minutes
   - Security scan: < 2 minutes

2. **Optimization Strategies**
   ```yaml
   Performance Improvements:
   - Parallel job execution
   - Selective test running
   - Build cache optimization
   - Resource allocation tuning
   ```

#### Bottleneck Identification
- Monitor job execution times
- Identify resource constraints
- Analyze dependency download times
- Review test execution patterns

### 5.4 Incident Response Procedures

#### Security Incident Protocol
1. **Immediate Response** (< 15 minutes)
   - Halt all deployments
   - Assess impact scope
   - Notify security team
   - Document incident details

2. **Investigation Phase** (< 2 hours)
   - Analyze security scan results
   - Review recent changes
   - Identify root cause
   - Assess data exposure risk

3. **Remediation Phase** (< 24 hours)
   - Implement security fixes
   - Update security policies
   - Notify stakeholders
   - Schedule post-incident review

#### Pipeline Outage Response
1. **Service Restoration**
   - Check CI service status
   - Verify runner availability
   - Test basic pipeline functionality
   - Communicate status to teams

2. **Backlog Management**
   - Prioritize critical PRs
   - Manual review fallback procedures
   - Resource reallocation
   - Timeline adjustment communication

## 6. Continuous Improvement Framework

### 6.1 Metrics and KPIs

#### Quality Metrics
- Defect escape rate: < 2%
- Test coverage: > 80%
- Security finding resolution time: < 48 hours
- Code review effectiveness: > 90%

#### Process Metrics
- Pipeline success rate: > 95%
- Average PR review time: < 4 hours
- Compliance violation rate: < 5%
- Override usage frequency: < 1%

### 6.2 Regular Assessment Schedule

#### Weekly Reviews
- Pipeline performance analysis
- Security scan result trends
- Process compliance metrics
- Team feedback collection

#### Monthly Assessments
- Full compliance audit
- Process improvement identification
- Tool effectiveness evaluation
- Training needs assessment

#### Quarterly Strategic Reviews
- Doctrine alignment verification
- Technology stack evaluation
- Process optimization opportunities
- Stakeholder satisfaction survey

---

## Appendix A: Emergency Contacts

- **Security Team**: security@circuittelligence.com
- **DevOps Team**: devops@circuittelligence.com
- **Architecture Team**: architecture@circuittelligence.com
- **Emergency Escalation**: emergency@circuittelligence.com

## Appendix B: Reference Documents

- [Security Policy Documentation](../security/security-policy.md)
- [Code Review Guidelines](../development/code-review-guidelines.md)
- [Deployment Procedures](../operations/deployment-procedures.md)
- [Incident Response Plan](../security/incident-response.md)

---

*Last Updated: September 11, 2025*  
*Document Owner: DevOps & Security Teams*  
*Review Cycle: Quarterly*
