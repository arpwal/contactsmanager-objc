# ContactsManager Objective-C SDK

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20macOS-lightgrey)](https://github.com/arpwal/contactsmanager-objc)
[![Version](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com/arpwal/contactsmanager-objc/releases)
[![Documentation](https://img.shields.io/badge/docs-contactsmanager.io-blue)](https://docs.contactsmanager.io)

ContactsManager.io is a powerful contact management solution designed specifically for consumer app builders. It provides a seamless, secure, and efficient way to manage user contacts across platforms while maintaining the highest standards of privacy and security.

📚 [Full Documentation](https://docs.contactsmanager.io)  
🚀 [Quick Start Guide](https://docs.contactsmanager.io/quickstart)

## Getting Started

### 1. Get Your API Key

1. Sign up or log in to the [ContactsManager Dashboard](https://dash.contactsmanager.io)
2. Create a new project or select an existing one
3. Navigate to the API Keys section
4. Create a new API key (takes less than 2 minutes)

Keep your API key secure and never expose it in client-side code.

### 2. Installation

#### Option 1: Using the Pre-built Framework

1. Download the latest `ContactsManager.framework` from the [Releases](https://github.com/arpwal/contactsmanager-objc/releases) page
2. Drag and drop the framework into your Xcode project
3. In your target's Build Phases, ensure the framework is added to "Link Binary With Libraries"
4. Add the following to your Info.plist to enable contact access:
   ```xml
   <key>NSContactsUsageDescription</key>
   <string>We need access to contacts to enable social features.</string>
   ```

#### Option 2: Using the Latest Framework

1. Download the latest framework from the `/Frameworks` directory in this repository
2. Follow steps 2-4 from Option 1

## Usage

### Initialization

```objc
#import <ContactsManager/ContactsManager.h>

// Create user info
CMUserInfo *userInfo = [[CMUserInfo alloc] init];
userInfo.userId = @"user123";
userInfo.email = @"user@example.com";  // Optional
userInfo.phone = @"+1234567890";       // Optional
userInfo.fullName = @"John Doe";       // Optional
userInfo.avatarUrl = @"https://...";   // Optional
userInfo.metadata = @{@"key": @"value"}; // Optional

// Initialize with options (optional)
CMContactsManagerOptions *options = [CMContactsManagerOptions defaultOptions];
options.restrictedKeysToFetch = @[@(CMContactDataRestrictionNotes)]; // Optional

// Initialize the service
[[CMContactService sharedInstance] initializeWithAPIKey:@"your_api_key"
                                                token:@"your_token" // Optional, will be generated if nil
                                             userInfo:userInfo
                                              options:options // Optional, uses defaults if nil
                                           completion:^(BOOL success, NSError * _Nullable error) {
    if (success) {
        NSLog(@"ContactsManager initialized successfully");
    } else {
        NSLog(@"Initialization failed: %@", error.localizedDescription);
    }
}];
```

### Fetching Contacts

```objc
// Fetch all contacts
[[CMContactService sharedInstance] fetchContactsWithCompletion:^(NSArray<CMContact *> * _Nullable contacts, NSError * _Nullable error) {
    if (contacts) {
        NSLog(@"Fetched %lu contacts", (unsigned long)contacts.count);
    }
}];

// Fetch contacts with specific field type
[[CMContactService sharedInstance] fetchContactsWithFieldType:CMContactFieldTypePhone
                                                  completion:^(NSArray<CMContact *> * _Nullable contacts, NSError * _Nullable error) {
    if (contacts) {
        NSLog(@"Fetched %lu contacts with phone numbers", (unsigned long)contacts.count);
    }
}];

// Fetch contacts in batches
[[CMContactService sharedInstance] fetchContactsWithBatchSize:20
                                                  batchIndex:0
                                                  completion:^(NSArray<CMContact *> * _Nullable contacts, NSError * _Nullable error) {
    if (contacts) {
        NSLog(@"Fetched batch of %lu contacts", (unsigned long)contacts.count);
    }
}];
```

### Additional Services

```objc
// Access social features
CMSocialService *socialService = [[CMContactService sharedInstance] socialService];

// Access contact recommendations
CMRecommendationService *recommendationService = [[CMContactService sharedInstance] recommendationService];

// Access contact search
CMContactSearchService *searchService = [[CMContactService sharedInstance] searchService];
```

## Features

- Automatic contact synchronization
- Background sync support
- Batch processing capabilities
- Comprehensive contact field support
- Social features integration
- Contact recommendations
- Advanced search capabilities
- Privacy-first approach
- Multi-platform support

## Requirements

- iOS 12.0+ / macOS 10.14+
- Xcode 13+
- ARC enabled

## Background Sync

The SDK automatically handles background sync of contacts. This includes:

- Sync when app becomes active
- Sync on contact store changes
- Background task scheduling
- Batch processing for optimal performance

## Error Handling

The SDK provides detailed error information through the `CMError` class, including:

- Initialization errors
- Contact access errors
- Database errors
- Network-related errors
- Validation errors

## Documentation & Resources

- [Full Documentation](https://docs.contactsmanager.io)
- [Quick Start Guide](https://docs.contactsmanager.io/quickstart)
- [API Reference](https://docs.contactsmanager.io/api-reference)
- [Dashboard](https://dash.contactsmanager.io)
- [Support](https://docs.contactsmanager.io/support)

## About ContactsManager.io

[ContactsManager.io](https://www.contactsmanager.io) provides a platform for app developers to integrate social features into their applications. Our SDK ensures that contact information stays with users only, with multi-layer encryption and military-grade security to prevent spam and data misuse.

For more information and documentation, visit [docs.contactsmanager.io](https://docs.contactsmanager.io).

## License

MIT License
