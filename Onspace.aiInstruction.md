## Key Implementation Notes
- The custom paywall must call actual RevenueCat purchase methods (`Purchases.purchasePackage()`)
- All subscription logic should rely on RevenueCat's entitlements system
- Ensure proper error handling through RevenueCat's provided methods
- **The paywall page must never use hardcoded SUBSCRIPTION_PLANS - always fetch live data from RevenueCat offerings and display it**

Check all the items below:
[ ] No hardcoded subscription plans anywhere in code
[ ] All pricing comes from live RevenueCat offerings
[ ] Custom paywall has both fixed and dynamic sections
[ ] Purchase flow calls actual RevenueCat purchase methods
[ ] Subscription status updates across app after purchase
[ ] Error handling for failed offering fetches
[ ] Platform-specific API key handling
[ ] Loading states during RevenueCat operations
