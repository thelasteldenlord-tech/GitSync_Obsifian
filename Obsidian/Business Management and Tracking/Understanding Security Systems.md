# Data Security & Privacy Framework

> A comprehensive guide to protecting client and company data

## Introduction

### Why This Matters

This framework is essential for:
- **Legal protection** - Avoiding lawsuits and regulatory penalties
- **Reputation management** - Building trust with clients and community
- **Operational security** - Protecting business assets and client information

Daily operations present opportunities for mistakes that could risk everything. This guide requires careful attention and regular review.

---

## Core Principles

### 1. Data is Sacred

**All data collected by our company must be handled with the highest level of privacy and security, regardless of how trivial it may seem.**

Key points:
- Every piece of information deserves protection
- Small mistakes can lead to significant legal liability
- Data security is not optional - it's foundational

### 2. Public Data Still Requires Protection

Even information available in the public domain must be treated as confidential when in our possession.

**Rationale**: Just because information exists publicly doesn't mean clients expect us to share it. While ethical research methods can uncover publicly available data through:
- Search engines
- Data aggregation sites
- Public records
- Legal research tools

...we commit to treating ALL client-related information as private.

### 3. Building Trust Through Actions

Our goal is simple: **Keep private information private.**

We aim to build a reputation where:
- Clients trust us with sensitive information
- Our integrity is beyond question
- Even in the event of mistakes, we respond with transparency and support
- We offer help, not exploitation

This trust becomes our most valuable business asset and spreads through reputation and referrals.

---

## Part 1: User and Group Structure

### The Principle of Least Privilege

**Core Concept**: Users only get the access they absolutely need to perform their job functions.

This minimizes risk by:
- Limiting potential damage from accidents
- Reducing insider threat exposure
- Simplifying access audits
- Ensuring compliance with privacy standards

---

### Recommended Group Structure

These groups are clear, descriptive, and map directly to organizational roles:

#### Group Definitions

| Group | Members | Access Level | Purpose |
|-------|---------|--------------|---------|
| **owners** | Business owners | Full access to everything | Ultimate control and oversight |
| **managers** | Management team | Most operational data | Daily operations management |
| **crew** | General staff | Task-specific documents only | Daily task execution |
| **confidential** | Select owners/managers | Highly sensitive data only | Protected information (credit, income, etc.) |

**Special Note on Confidential Group**: This is a restricted group for highly sensitive documents such as client credit information, financial records, or personal data. Membership is strictly limited to those with legitimate business need.

---

### Username Conventions

Keep usernames simple and consistent for easy management:

**Format Examples**:
- **Owners**: `john`, `jane`
- **Managers**: `mgr_alex`, `mgr_sam`
- **Crew**: `crew_taylor`, `crew_riley`

**Benefits of this system**:
- Easy to identify user roles at a glance
- Simple to remember
- Scales as business grows

---

## Part 2: Directory Structure and Access Policy

### Logical Organization

A well-organized directory structure makes security management intuitive and reduces errors.

**Base Directory**: `/company_data/`

```
/company_data/
├── admin/                      Administrative & sensitive business data
│   ├── financials/             Company financial records
│   ├── legal/                  Legal documents and contracts
│   └── hr/                     Human resources and personnel
│
├── operations/                 Day-to-day operational data
│   ├── schedules/              Work schedules and assignments
│   ├── procedures/             Standard operating procedures
│   └── internal_comm/          Internal communications
│
└── clients/                    Client-related information
    ├── prospects/              Prospect information (less sensitive)
    │   └── highly_sensitive/   PII, credit, financial (RESTRICTED)
    └── active/                 Active client data (contact info, projects)
```

---

### Permission Model Reference

**Understanding chmod numbers**:
- `7` = read/write/execute (rwx) - Full control
- `5` = read/execute (r-x) - Can view and access, cannot modify
- `0` = no access (---) - Completely restricted

**Permission format**: `owner-group-other`
- Example: `750` = owner: rwx, group: r-x, other: none

---

### Access Control Matrix

| Directory | Owner | Group | chmod | Policy Explanation |
|-----------|-------|-------|-------|-------------------|
| `/company_data` | root | root | 755 | Root-owned top level. All can list, only privileged can modify |
| `admin/` | root | owners | 770 | **Owners only**. Managers & Crew: no access |
| `admin/financials` | root | owners | 750 | Owners: full. Managers: read-only |
| `admin/legal` | root | owners | 770 | **Owners only** - strictly confidential |
| `admin/hr` | root | managers | 750 | Owners & Managers. Crew: no access |
| `operations/` | root | managers | 775 | Owners & Managers: full. Crew: can enter/list |
| `operations/schedules` | root | crew | 775 | **All staff**: read & write |
| `operations/procedures` | root | crew | 755 | Managers: update. Crew: read-only |
| `clients/` | root | managers | 750 | **Owners & Managers only** |
| `clients/prospects` | root | managers | 750 | **Owners & Managers only** |
| `clients/prospects/highly_sensitive` | root | confidential | 770 | **CRITICAL**: Confidential group ONLY |

**Critical Note**: The `highly_sensitive` directory requires extra attention. This is where PII (Personally Identifiable Information), credit reports, income data, and similar sensitive information is stored.

---

## Part 3: Implementation Guide

### Prerequisites

Before implementing this system:
- Have root/sudo access to your system
- Know which users need to be in which groups
- Back up any existing data
- Test on a non-production system first (recommended)

**Important**: Use `sudo` for all these commands.

---

### Step 1: Create Groups and Users

```bash
# Create the groups
sudo groupadd owners
sudo groupadd managers
sudo groupadd crew
sudo groupadd confidential

# Add users to groups. A user can be in multiple groups.
sudo usermod -aG owners john
sudo usermod -aG owners jane

sudo usermod -aG managers mgr_alex
sudo usermod -aG managers mgr_sam

sudo usermod -aG crew crew_taylor
sudo usermod -aG crew crew_riley

# Add specific people to the confidential group (e.g., you and one manager)
sudo usermod -aG confidential john
sudo usermod -aG confidential jane
sudo usermod -aG confidential mgr_alex  # Only if this manager needs to see credit info
```

**Note**: A user can belong to multiple groups. The `-aG` flag adds them to a group without removing them from existing groups.

---

### Step 2: Create the Directory Structure

```bash
sudo mkdir -p /company_data/{admin/financials,admin/legal,admin/hr,operations/schedules,operations/procedures,operations/internal_comm,clients/prospects/highly_sensitive,clients/active}
```

**What this does**: Creates the entire directory tree in a single command using brace expansion.

---

### Step 3: Apply Ownership and Permissions

This is the critical step where the security policy is enforced. Follow the access control matrix from Part 2.

```bash
# Top level - safe and neutral
sudo chown root:root /company_data
sudo chmod 755 /company_data

# Admin section
sudo chown root:owners /company_data/admin
sudo chmod 770 /company_data/admin

sudo chown root:owners /company_data/admin/financials
sudo chmod 750 /company_data/admin/financials

sudo chown root:owners /company_data/admin/legal
sudo chmod 770 /company_data/admin/legal

sudo chown root:managers /company_data/admin/hr
sudo chmod 750 /company_data/admin/hr

# Operations section
sudo chown root:managers /company_data/operations
sudo chmod 775 /company_data/operations

sudo chown root:crew /company_data/operations/schedules
sudo chmod 775 /company_data/operations/schedules

sudo chown root:crew /company_data/operations/procedures
sudo chmod 755 /company_data/operations/procedures # Crew can read, managers can write

# Clients section
sudo chown root:managers /company_data/clients
sudo chmod 750 /company_data/clients

sudo chown root:managers /company_data/clients/prospects
sudo chmod 750 /company_data/clients/prospects

# The most sensitive directory
sudo chown root:confidential /company_data/clients/prospects/highly_sensitive
sudo chmod 770 /company_data/clients/prospects/highly_sensitive
```

---

## Part 4: Verification and Best Practices

### Security Verification

It's essential to verify that permissions are correctly applied. Here's how to check your work.

#### Verification Commands

**Check user group membership**:
```bash
groups john
```
Expected output: `john : john owners confidential`

**Check directory permissions**:
```bash
ls -ld /company_data/clients/prospects/highly_sensitive
```
Expected output: `drwxrwx--- 2 root confidential 4096 ...`

This confirms:
- `drwxrwx---` = owner (rwx), group (rwx), other (no access)
- `root confidential` = owned by root, group is confidential

**Test access as different users**:
```bash
# This should FAIL for mgr_sam (not in 'confidential' group)
sudo -u mgr_sam ls -l /company_data/clients/prospects/highly_sensitive
# Expected: ls: cannot open directory ...: Permission denied

# This should WORK for mgr_alex (in 'confidential' group)
sudo -u mgr_alex ls -l /company_data/clients/prospects/highly_sensitive
# Expected: Directory listing displayed
```

---

### Critical Security Rules

#### What to NEVER Do

1. **NEVER use `chmod 777`**
   - This gives everyone full access
   - Creates a massive security vulnerability
   - No legitimate business use case

2. **Be extremely careful with `chmod -R` (recursive)**
   - Double-check your path before executing
   - Can irreversibly change permissions on hundreds of files
   - One typo can expose sensitive data

3. **Keep the 'owners' group small**
   - This is your business "root" access
   - Only absolutely trusted individuals
   - Review membership regularly

4. **Never share credentials**
   - Each person gets their own account
   - No "shared" passwords
   - Enable accountability and auditing

---

### Advanced: The SetGID Bit

**Purpose**: Automatically inherit group ownership on new files.

**Problem**: When a user creates a file, it normally inherits their primary group. In shared directories, this can cause access issues.

**Solution**: The SetGID bit forces new files to inherit the directory's group.

```bash
# Example: For the operations/schedules folder
sudo chmod g+s /company_data/operations/schedules
```

**How it works**:
- When `john` (group: owners) creates a file in schedules
- The file's group automatically becomes `crew` (the directory's group)
- No manual `chown` needed
- Perfect for shared collaborative spaces

**Verify SetGID**:
```bash
ls -ld /company_data/operations/schedules
# Look for 's' in group permissions: drwxrwsr-x
```

---

## Summary and Next Steps

### What You've Accomplished

By implementing this framework, you have:

1. **Established a security-first culture** - Data protection is now foundational
2. **Minimized legal liability** - Proper access controls reduce exposure
3. **Built trust** - Clients can rely on your discretion
4. **Created scalability** - This system grows with your business
5. **Enabled accountability** - Audit trails show who accessed what

### Security is Superior to Convenience

This system is **far more secure** than:
- Shared drives with no access controls
- Files on personal computers
- Email attachments
- "Everyone can access everything" approaches

By thinking in terms of **groups** and **deliberate permissions**, you've dramatically reduced the risk of sensitive data exposure.

---

### Ongoing Maintenance

#### Regular Reviews (Quarterly)
- [ ] Review user group memberships
- [ ] Audit sensitive directory access
- [ ] Remove access for departed employees
- [ ] Verify permission settings haven't changed

#### When Changes Occur
- **New employee**: Add to appropriate groups only
- **Role change**: Update group memberships
- **Departure**: Remove from all groups immediately
- **New data type**: Assess sensitivity, place accordingly

---

### Growth and Adaptation

**This system is designed to scale**:
- Add new groups as needed (e.g., `finance`, `hr_admin`)
- Create subdirectories for new business areas
- Adjust permissions as requirements evolve
- Document changes in [[Policies/Access Control Log]]

---

### Additional Security Measures

Consider implementing:
- [ ] Encrypted backups
- [ ] File integrity monitoring
- [ ] Access logging and auditing
- [ ] Two-factor authentication for sensitive systems
- [ ] Regular security training for staff
- [ ] Incident response procedures

See [[Policies/Security Roadmap]] for additional enhancements.

---

## Related Documents

- [[Data Privacy Policy]] - How we handle client data
- [[Client Access Policy]] - Access authorization procedures
- [[Policies/Incident Response]] - What to do if security is compromised

---

## Conclusion

**You've built something solid**. This framework provides strong protection while remaining manageable for a small business. Start here, gain confidence, and expand as needed.

Remember: **Security is a journey, not a destination**. Regular review and continuous improvement will keep your business and clients protected.

---

*Last Updated: 2025-10-28*
*Next Review: 2026-01-28*