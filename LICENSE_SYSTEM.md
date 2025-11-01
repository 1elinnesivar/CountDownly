# License Key System Documentation

## Overview

CountDownly uses a license key system to differentiate between free and premium users. Free users are limited to 3 countdowns, while premium users have unlimited access.

## License Key Format

License keys follow this format:
```
CDLY-XXXX-XXXX-XXXX
```

Example: `CDLY-A1B2-C3D4-E5F6`

## How It Works

1. **Free Users**:
   - Can create up to 3 countdowns
   - See a reminder showing remaining countdowns
   - After 3 countdowns, must upgrade to continue

2. **Premium Users**:
   - Unlimited countdowns
   - License key stored in browser localStorage
   - "Premium Active" badge shown

## Generating License Keys

Since this is a static site, you have several options for generating and distributing license keys:

### Option 1: Gumroad Email Automation (Recommended)

1. Go to your Gumroad product settings
2. Set up an email automation that sends after purchase
3. Include a license key in the email

**Email Template Example:**
```
Thank you for purchasing CountDownly Premium!

Your license key: CDLY-XXXX-XXXX-XXXX

To activate:
1. Visit: https://yourdomain.com/license.html
2. Enter your license key
3. Start creating unlimited countdowns!

If you have any questions, please contact support.
```

### Option 2: License Key Generator Script

Create a simple PHP/Python script to generate license keys:

**PHP Example:**
```php
<?php
function generateLicenseKey() {
    $prefix = 'CDLY';
    $part1 = strtoupper(substr(md5(uniqid(rand(), true)), 0, 4));
    $part2 = strtoupper(substr(md5(uniqid(rand(), true)), 0, 4));
    $part3 = strtoupper(substr(md5(uniqid(rand(), true)), 0, 4));
    return $prefix . '-' . $part1 . '-' . $part2 . '-' . $part3;
}

echo generateLicenseKey();
```

**Python Example:**
```python
import random
import string

def generate_license_key():
    prefix = 'CDLY'
    chars = string.ascii_uppercase + string.digits
    part1 = ''.join(random.choice(chars) for _ in range(4))
    part2 = ''.join(random.choice(chars) for _ in range(4))
    part3 = ''.join(random.choice(chars) for _ in range(4))
    return f'{prefix}-{part1}-{part2}-{part3}'

print(generate_license_key())
```

### Option 3: Gumroad Download File

1. Create a text file with the license key for each purchase
2. Upload it as a download file in Gumroad
3. Gumroad will automatically provide it after purchase

## Validation

Currently, license keys are validated client-side using format validation:
- Format: `CDLY-XXXX-XXXX-XXXX` (where X is alphanumeric)
- Stored in browser localStorage
- No server-side validation (static site limitation)

### For Production (Recommended):

For better security, implement server-side validation:
1. Store valid license keys in a database
2. Create an API endpoint to validate keys
3. Update `license.html` to call this API
4. Track license usage and prevent sharing

## Manual License Key Distribution

If you need to manually provide license keys:

1. Generate a key using one of the methods above
2. Send it to the customer via email or message
3. Customer enters it at: `https://yourdomain.com/license.html`

## License Key Management

### Viewing User License Status

Check browser localStorage:
```javascript
localStorage.getItem('countdownly_license')
```

### Resetting License (for testing)

```javascript
localStorage.removeItem('countdownly_license');
localStorage.removeItem('countdownly_countdown_count');
```

### Free User Countdown Count

```javascript
localStorage.getItem('countdownly_countdown_count')
```

## Security Considerations

**Current Implementation (Client-Side Only):**
- ⚠️ License keys can be shared between users
- ⚠️ Users can manually add keys to localStorage
- ⚠️ No server-side validation

**Recommended Improvements:**
- ✅ Implement server-side validation API
- ✅ Track license key usage by domain/IP
- ✅ Limit licenses to specific email addresses
- ✅ Add expiration dates for licenses
- ✅ Use cryptographic signing for license keys

## Gumroad Integration

### Setting Up Email Automation:

1. Go to Gumroad Dashboard
2. Select your CountDownly product
3. Go to "Email" or "Automatizations" section
4. Create a post-purchase email
5. Include the license key in the email template

### Alternative: Product Download File

1. Generate a unique license key file for each customer
2. Upload as a download file in Gumroad
3. Gumroad provides it automatically after purchase

## Support

If customers lose their license key:
- They can check their Gumroad purchase receipt
- You can look up their purchase in Gumroad dashboard
- Regenerate and send a new key if needed

