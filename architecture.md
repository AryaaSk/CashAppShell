So let’s assume I (the developer and prompter) know the exact architecture of an app in my head,

How do I make an LLM agent write the whole app with a deterministically-robust approach?

Encapsulation and abstraction are key. You want to keep the different components as loosely coupled as possible. For example, we use an APIService to communicate between the frontend and backend, or we use a RevenueCatService to handle everything related to revenuecat.

Managing state within an app is a big issue, it can really confuse you if you don’t stay on top of it. Using global variables can solve this, but they come with their own set of challenges. Nonetheless, storing all user state in a UserService would likely be ideal to keep the app structure tidy and views decoupled from actual logic.

A rule of thumb should be to not perform much logic within the Views themselves, the views should simply be used as templates to present data.

A big slowdown is also the entire onboarding flow; since these screens are special in the fact that they generally are only shown once, they likely should also have their own service (to store state such as ‘onboardingShown’); alternatively, the onboarding state can just be stored in the same UserService mentioned above.

Subscriptions and purchases: subscriptions and other in app purchases should generally be handled by the revenuecat service, which is then imported into the User service to create wrapper functions around; this means no other file should import the revenuecat service, instead just use the wrapper functions from the UserService


Also, its important to reference the standard apple EULA for subscriptions and include a restore purchase button or the app will be rejected.
Apple Standard EULA: https://www.apple.com/legal/internet-services/itunes/dev/stdeula/

Guideline 3.1.2:
Apps offering auto-renewable subscriptions must include all of the following required information in the binary:

- Title of auto-renewing subscription (this may be the same as the in-app purchase product name)
- Length of subscription
- Price of subscription, and price per unit if appropriate
- Functional links to the privacy policy and Terms of Use (EULA)

The app metadata must also include functional links to the privacy policy in the Privacy Policy field in App Store Connect and the Terms of Use (EULA) in the App Description or EULA field in App Store Connect.

Guideline 3.1.1

The app offers in-app purchases that can be restored but does not include a "Restore Purchases" feature to allow users to restore the previously purchased in-app purchases.

Next Steps

To restore previously purchased in-app purchase products, it would be appropriate to provide a distinct "Restore" button and initiate the restore process when the "Restore" button is tapped by the user. Note that automatically restoring purchases on launch will not resolve this issue.




The backend generally follows Springboot structure (services, controllers, DTOs, etc…) so it remains fairly well structured.

Same with web, the NextJS structure accurately reflects the website architecture so it is relatively well structured from the beginning.
