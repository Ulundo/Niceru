I'm building a mobile app for browsing DOG pictures. The app should have two tabs: Feed and Profile.

In the Feed tab:
- Display a vertical scrollable list of 10 DOG images.
- Only the first 2 images should be fully visible. The remaining 8 images must have a semi-transparent overlay with the text: "Subscribe to unlock" centered over the image.
- Tapping on a locked image should present a **custom RevenueCat paywall screen** with a fixed header section and dynamic subscription plans.

# RevenueCat Integration Template

## Installation Requirements
- Install `react-native-purchases` using version 8.11.4 or higher
- Install `react-native-purchases-ui` using version 8.11.4 or higher
- Ensure libraries are compatible with Expo Go

## Core Integration Components

### 1. SDK Configuration Hook
- Create and export a custom hook called `initializePurchases`
- Use the actual `Purchases.configure()` method to configure the RevenueCat SDK
- **Guide users to manually store their RevenueCat public API key in a .env file using format: `EXPO_PUBLIC_REVENUECAT_PUBLIC_SDK_KEY=Revenuecat Public API Key`**
- Initialize this hook in your app's main layout file (e.g., `_layout.tsx`)

### 2. Subscription Status Hook
- Create and export a hook called `useSubscriptionStatus`
- Use `Purchases.getCustomerInfo()` to check user's subscription status
- Implement entitlements logic to determine subscription state
- Return a boolean `isSubscribed` value

### 3. Custom Paywall Implementation
- **Create a custom paywall page with two distinct sections:**
- **Fixed header section**: Display static content like app branding and benefit to subscribe. 
- **Dynamic subscription plans section**: Fetch and display real-time RevenueCat offerings
- **Dynamically fetch offerings and products from RevenueCat** - do not use hardcoded SUBSCRIPTION_PLANS
- Use `Purchases.getOfferings()` to retrieve current available products and offerings
- Ensure the paywall displays actual products configured in your RevenueCat dashboard
- **Create custom purchase buttons that integrate with RevenueCat purchase methods**
- Design subscription plan cards that show dynamic pricing, duration, and features from RevenueCat
- **Never use hardcoded product data** - all subscription information must come from live RevenueCat offerings

### 4. Content Protection Logic
- Use the `useSubscriptionStatus` hook across your app to control content access
- Show/hide locked content based on subscription status
- Display custom paywall when users attempt to access premium content

### 5. Dynamic Product Configuration
- **Never use hardcoded product lists or SUBSCRIPTION_PLANS arrays**
- Always fetch current offerings using `Purchases.getOfferings()`
- Parse offering data to extract product titles, prices, billing periods, and descriptions
- Let RevenueCat manage product availability and pricing dynamically
- Ensure the app adapts to changes in your RevenueCat dashboard configuration
- Handle offering retrieval errors gracefully with loading states and fallbacks

## Implementation Guidelines

### Technical Constraints
- **Use real RevenueCat methods** - do not mock purchase or subscription logic
- Ensure compatibility with Expo Go environment
- Keep code modular with well-named components
- No backend integration or persistent storage required - rely on RevenueCat SDK only

### UI/UX Requirements
- Display locked content with semi-transparent overlay
- Center "Subscribe to unlock" text over locked content
- Present custom RevenueCat paywall when locked content is tapped
- Show subscription status in user interface
- Custom paywall must have fixed branding section + dynamic offerings section
