---
Name: MD5 Exception Troubleshooting
---

# MD5 Exception

## Problem

You execute a method from the Bulk Operations library, and the following error is thrown:

> This implementation is not part of the Windows Platform FIPS validated cryptographic algorithms.

## Solution

### Cause

The default algorithm to validate the license key & name is not supported with FIPS enabled.

### Fix

#### Ask for a compatible key

Contact us and we will send you a new key supporting FIPS: <a href="mailto:info@zzzprojects.com">info@zzzprojects.com</a>

Why don't we generated key compatible with FIPS by default? Because it will not be supported for a client machine with Windows XP or below.

#### Disable FIPS

Article: [Disable FIPS](https://docs.trendmicro.com/all/ent/sc/v3.0/en-US/cmcolh/t_fips.html){:target="_blank"}
