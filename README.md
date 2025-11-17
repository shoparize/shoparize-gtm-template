# Shoparize Partner Tracking - Google Tag Manager Template

Official Google Tag Manager custom template for Shoparize partner tracking. This template provides a secure, compliant way to track conversions and clicks without triggering malware alerts.

## 🎯 Why Use This Template?

Google Tag Manager's security scanner may flag custom HTML tags that load external scripts as potential malware. This custom template:

✅ **Prevents malware alerts** - Uses GTM's built-in APIs  
✅ **Google recommended** - Follows official best practices  
✅ **Secure by design** - Sandboxed execution environment  
✅ **Easy to configure** - Simple UI with validation  
✅ **Fully featured** - All tracking capabilities included  

## 🚀 Quick Start

### Prerequisites

- Active Google Tag Manager account
- Shoparize Partner Shop ID
- Basic understanding of GTM concepts (tags, triggers, variables)

### Installation

#### Step 1: Import the Template

1. Download `shoparize-gtm-template.tpl` from this repository
2. Log into [Google Tag Manager](https://tagmanager.google.com/)
3. Select your container
4. Go to **Templates** (left sidebar)
5. In the **Tag Templates** section, click **New**
6. Click the **⋮** (three dots) in the top right corner
7. Select **Import**
8. Upload `shoparize-gtm-template.tpl`
9. Click **Save**

#### Step 2: Create Click Tracking Tag

1. Go to **Tags** → **New**
2. Click **Tag Configuration**
3. Select **Shoparize Partner Tracking** (your new template)
4. Configure:
   - **Tracking Type**: `Initialize Click Tracking`
   - **Shop ID**: Your Shoparize shop ID (e.g., `3331`)
5. Set **Triggering** to: `All Pages`
6. Name: `Shoparize - Click Tracking`
7. Click **Save**

#### Step 3: Create Conversion Tracking Tag

1. Go to **Tags** → **New**
2. Click **Tag Configuration**
3. Select **Shoparize Partner Tracking**
4. Configure:
   - **Tracking Type**: `Conversion Tracking`
   - **Shop ID**: Your Shoparize shop ID
   - **Transaction ID**: `{{Your Order ID Variable}}`
   - **Order Value**: `{{Your Order Value Variable}}`
   - **Tax Amount**: `{{Your Tax Variable}}`
   - **Shipping Cost**: `{{Your Shipping Variable}}`
   - **Currency**: `EUR` (or your currency)
   - **Order Items**: `{{Your Items Variable}}`
   - ☑️ **Send conversion only for Shoparize traffic**: Check this
5. Set **Triggering** to: Your purchase confirmation trigger
6. Name: `Shoparize - Conversion Tracking`
7. Click **Save**

#### Step 4: Test & Publish

1. Click **Preview** in GTM
2. Visit your website with `?utm_source=shoparize` parameter
3. Verify the click tracking tag fires
4. Complete a test purchase
5. Verify the conversion tag fires
6. If all looks good, click **Submit** → **Publish**

## 📋 Configuration Options

### Tracking Type

**Initialize Click Tracking**
- Tracks when users arrive from Shoparize
- Sets tracking cookies for attribution
- Required on all pages

**Conversion Tracking**
- Tracks completed purchases
- Sends transaction data to Shoparize
- Required on order confirmation page only

### Required Fields

| Field | Description | Example |
|-------|-------------|---------|
| **Shop ID** | Your unique Shoparize partner ID | `3331` |

### Conversion Data Fields

| Field | Description | Required | Example |
|-------|-------------|----------|---------|
| **Transaction ID** | Unique order identifier | Yes | `ORDER-12345` |
| **Order Value** | Total order amount | Yes | `99.99` |
| **Tax Amount** | Tax/VAT amount | No | `19.00` |
| **Shipping Cost** | Shipping fee | No | `5.99` |
| **Currency** | Three-letter currency code | Yes | `EUR` |
| **Order Items** | Array of purchased items | No | `[{...}]` |

### Advanced Options

**Send conversion only for Shoparize traffic**
- When checked: Only sends conversions for users who came from Shoparize
- When unchecked: Sends all conversions
- **Recommended**: Keep checked to avoid inflating conversion numbers

## 🔧 Setting Up Variables

The template works with GTM variables. Here's how to set them up:

### 1. Data Layer Variables

Create these variables to pull data from your data layer:

```javascript
// On your order confirmation page
window.dataLayer.push({
  'orderId': 'ORDER-12345',
  'orderValue': 99.99,
  'orderTax': 19.00,
  'orderShipping': 5.99,
  'orderCurrency': 'EUR',
  'orderItems': [
    {
      'id': 'PROD-123',
      'name': 'Product Name',
      'price': 99.99,
      'quantity': 1
    }
  ]
});
```

Then create GTM Data Layer Variables:
- Name: `DLV - Order ID` → Data Layer Variable: `orderId`
- Name: `DLV - Order Value` → Data Layer Variable: `orderValue`
- etc.

### 2. Using the Variables

In the conversion tracking tag, reference your variables:
- Transaction ID: `{{DLV - Order ID}}`
- Order Value: `{{DLV - Order Value}}`
- Tax Amount: `{{DLV - Order Tax}}`
- etc.

## 🧪 Testing

### Test Click Tracking

1. In GTM Preview mode, visit:
   ```
   https://your-website.com/?utm_source=shoparize&utm_medium=affiliate
   ```

2. Check **Tag Assistant**:
   - ✅ "Shoparize - Click Tracking" should fire
   - ✅ Status should be "Succeeded"

3. Check **Browser Console** (F12):
   - ✅ Look for: `Shoparize: Click tracked successfully`

4. Check **Browser Cookies** (DevTools → Application → Cookies):
   - ✅ `_partner_click_time`
   - ✅ `_partner_utm_source`
   - ✅ `_partner_utm_medium`

### Test Conversion Tracking

1. Complete a test purchase on your site
2. On order confirmation page, check **Tag Assistant**:
   - ✅ "Shoparize - Conversion Tracking" should fire
   - ✅ Status should be "Succeeded"

3. Check **Browser Console**:
   - ✅ Look for: `Shoparize: Conversion tracked successfully`

4. Check **Network Tab** (F12 → Network):
   - ✅ Look for request to: `partner.shoparize.com/api/incoming/conv`
   - ✅ Verify payload contains transaction data

## 🔍 Debugging

### Tag Not Firing?

**Check triggers:**
- Is the trigger configured correctly?
- Does the page match the trigger conditions?
- Use GTM Preview mode to see which triggers fire

**Check variables:**
- Are your variables returning values?
- In Preview mode, click on the tag and check "Variables"
- Make sure data layer variables exist before the tag fires

### Conversion Not Tracking?

**Check Shoparize traffic:**
- User must have `utm_source=shoparize` in their original visit
- Check if `_partner_utm_source` cookie exists
- If "Send only for Shoparize traffic" is checked, non-Shoparize users won't track

**Check data layer:**
- Verify your data layer contains transaction data
- Data layer must be pushed BEFORE the tag fires
- Use console.log(dataLayer) to inspect

### API Request Failing?

**Check browser console:**
- Look for network errors
- Verify API endpoint is accessible
- Check if CORS is enabled

**Check API response:**
- Network tab → Find the request
- Check response status (should be 200)
- Verify response body

## 🛡️ Security & Privacy

### Permissions

The template requests these GTM permissions:

- **Logging** (debug mode only) - For troubleshooting
- **Send Pixel** - To send tracking data to Shoparize API
- **Get Cookies** - To read partner tracking cookies
- **Set Cookies** - To store tracking attribution data
- **Get URL** - To read URL parameters (utm_source, etc.)

### Data Collection

The template collects:

**Click Tracking:**
- UTM parameters (source, medium, campaign, term)
- Click IDs (gclid, msclkid, wbraid, gbraid)
- Timestamp of click
- Shop ID

**Conversion Tracking:**
- All click tracking data (from cookies)
- Transaction ID
- Order value, tax, shipping
- Currency
- Order items (if provided)
- Timestamp of conversion

### Cookie Usage

All cookies are first-party cookies set on your domain:

| Cookie | Purpose | Expiration |
|--------|---------|------------|
| `_partner_click_time` | Attribution timestamp | 30 days |
| `_partner_utm_*` | Marketing attribution | 30 days |
| `_partner_gclid` | Google Click ID | 30 days |
| `_partner_msclkid` | Microsoft Click ID | 30 days |

## 🚨 Troubleshooting

### "Malware Flagged" Alert

If you see this alert after importing the template:

1. **Don't panic** - The template itself is safe
2. **Check the file** - Make sure you imported the `.tpl` file, not a `.js` file
3. **Re-scan** - GTM will automatically re-scan after 24-48 hours
4. **Contact GTM support** - If the issue persists, request a manual review

### Template Not Appearing

1. Make sure you imported in the **Tag Templates** section (not Variable Templates)
2. Refresh your browser
3. Check if import succeeded (no error messages)
4. Try re-importing

### Variables Not Working

1. Verify the data layer variable names match exactly
2. Check that data is pushed to the data layer before the tag fires
3. Use GTM Preview mode to inspect variable values
4. Consider using Tag Sequencing if timing is an issue

## 📊 Monitoring & Maintenance

### Regular Checks

- **Weekly**: Review conversion data in Shoparize dashboard
- **Monthly**: Check GTM for errors or warnings
- **After site updates**: Test tracking still works

### Version Control

- Keep a copy of your template file
- Document any customizations
- Export GTM container versions regularly

### Updates

Check this repository for template updates:
- Bug fixes
- New features
- API changes

## 🔄 Migration from Custom HTML Tags

If you're migrating from old Custom HTML tags:

1. **Keep old tags active** during transition
2. **Import and test** the new template in Preview mode
3. **Run both** for a few days to compare data
4. **Disable old tags** once confident
5. **Delete old tags** after verification period

## 📞 Support

### Documentation

- [Complete GTM Malware Fix Guide](https://github.com/shoparize/partnerjs/blob/main/GTM_MALWARE_FIX_GUIDE.md)
- [GTM Custom Templates Documentation](https://developers.google.com/tag-platform/tag-manager/templates)

### Getting Help

1. **Check the logs**: Browser console and GTM debug console
2. **Review this README**: Most issues are covered here
3. **Contact support**: Email partner-support@shoparize.com
4. **GitHub Issues**: Report bugs or request features

## 📝 License

ISC License

## 🙏 Credits

Created by Shoparize for our partner network.

Based on Google Tag Manager's custom template framework.

## 📚 Additional Resources

- [Google Tag Manager Documentation](https://developers.google.com/tag-manager)
- [GTM Custom Template Best Practices](https://developers.google.com/tag-platform/tag-manager/templates/best-practices)
- [GTM Community Template Gallery](https://tagmanager.google.com/gallery/)
- [Shoparize Partner Documentation](https://partner.shoparize.com/docs)

---

**Version**: 1.0.0  
**Last Updated**: November 2025  
**Compatibility**: GTM Web Containers

