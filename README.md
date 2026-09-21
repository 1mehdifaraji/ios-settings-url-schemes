iOS Settings URL Schemes 

A collection of known iOS Settings URL schemes, including legacy prefs:, App-prefs:, and newer settings-navigation:// destinations.

Latest update: September 21, 2026

This repository preserves older URLs for historical/reference purposes and adds newer destinations observed on modern iOS versions.

⸻

⚠️ Important

Most URLs in this repository are undocumented/private iOS implementation details.

Apple does not guarantee that these URLs will continue to work across iOS releases.

Their behavior can differ depending on:

- iOS version
- Settings app changes
- whether the URL is opened from an app, Safari, or Shortcuts
- device configuration
- installed apps
- region
- whether the destination is available on the device

A URL working in Shortcuts does not necessarily mean that the same URL can be used successfully from a third-party application.

For App Store applications, prefer Apple’s documented APIs whenever one exists.

⸻

Contents

- Official Apple APIs
- URL Scheme Types
- Settings URLs
  - Apple Account
  - Airplane Mode
  - Wi-Fi
  - Bluetooth
  - Mobile Service
  - Personal Hotspot
  - VPN
  - Notifications
  - Sounds & Haptics
  - Focus
  - Screen Time
  - General
  - Accessibility
  - Privacy & Security
  - Battery
  - Display & Brightness
  - Wallpaper
  - Siri
  - Face ID & Passcode
  - Emergency SOS
  - Privacy
  - App Store
  - Wallet & Apple Pay
  - Passwords
  - Safari
  - Mail
  - Messages
  - Phone
  - Contacts
  - Calendar
  - Notes
  - Photos
  - Music
  - Podcasts
  - Maps
  - Health
  - Home
  - News
  - TV
  - Developer
  - Weather
  - Freeform
  - Journal
- Legacy / Historical URLs
- Known Changes
- iOS 26+
- iOS 27
- Testing
- Contributing
- License

⸻

Official Apple APIs

Whenever possible, use Apple’s public APIs instead of undocumented Settings URLs.

Open your application’s Settings

if let url = URL(string: UIApplication.openSettingsURLString) {
await UIApplication.shared.open(url)
}

This opens:

Settings → Your App

⸻

Open your application’s notification settings

if let url = URL(string: UIApplication.openNotificationSettingsURLString) {
await UIApplication.shared.open(url)
}

⸻

Open Default Apps settings

> ⚠️ Deprecated: Apple currently documents `openDefaultApplicationsSettingsURLString` as deprecated.
> Keep this reference for historical/API compatibility documentation rather than new code.

if let url = URL(string: UIApplication.openDefaultApplicationsSettingsURLString) {
await UIApplication.shared.open(url)
}

⸻

Safari Extensions

For Safari Web Extensions, use Apple’s Safari settings API when applicable instead of relying on a private URL:

SFSafariSettings.openExtensionsSettings(
forIdentifiers: ["com.example.extension"]
)

⸻

Call Blocking & Identification

Call Directory extensions can use Apple’s API:

try await CXCallDirectoryManager.sharedInstance.openSettings()

⸻

URL Scheme Types

There are several URL formats that have been observed across iOS releases.

prefs:

Example:

prefs:root=WIFI

This is an undocumented/private scheme.

⸻

App-prefs:

Example:

App-prefs:root=WIFI

This is also undocumented/private.

Some older iOS versions and workflows used App-prefs: interchangeably with prefs:.

⸻

settings-navigation://

Example:

settings-navigation://com.apple.Settings.PrivacyAndSecurity

This scheme is used by newer versions of Settings, including iOS 26-era Settings navigation.

It is not a public Apple API.

⸻

Settings URLs

Apple Account

Apple Account

prefs:root=APPLE_ACCOUNT
App-prefs:root=APPLE_ACCOUNT

Password & Security

prefs:root=APPLE_ACCOUNT&path=PASSWORD_AND_SECURITY
settings-navigation://com.apple.Settings.AppleAccount/PASSWORD_AND_SECURITY

Payment & Shipping

prefs:root=APPLE_ACCOUNT&path=PAYMENT_AND_SHIPPING
settings-navigation://com.apple.Settings.AppleAccount/PAYMENT_AND_SHIPPING

Subscriptions

prefs:root=APPLE_ACCOUNT&path=SUBSCRIPTIONS
settings-navigation://com.apple.Settings.AppleAccount/SUBSCRIPTIONS

iCloud

prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE

iCloud Storage

prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/STORAGE_AND_BACKUP

Name, Phone Numbers, Email

prefs:root=APPLE_ACCOUNT&path=APPLE_ACCOUNT_CONTACT

Share My Location

prefs:root=APPLE_ACCOUNT&path=LOCATION_SHARING

Family

prefs:root=APPLE_ACCOUNT&path=Family

⸻

Airplane Mode

prefs:root=AIRPLANE_MODE
App-prefs:root=AIRPLANE_MODE

⸻

Wi-Fi

prefs:root=WIFI
App-prefs:root=WIFI

⚠️ iOS 26+

Direct programmatic navigation to Wi-Fi settings has become unreliable in newer iOS versions.

Keep this URL for historical/reference purposes.

⸻

Bluetooth

prefs:root=Bluetooth
App-prefs:root=Bluetooth

⸻

Mobile Service

prefs:root=MOBILE_DATA_SETTINGS_ID
App-prefs:root=MOBILE_DATA_SETTINGS_ID

Mobile Data

prefs:root=MOBILE_DATA_SETTINGS_ID

Personal Hotspot

prefs:root=INTERNET_TETHERING
App-prefs:root=INTERNET_TETHERING

⚠️ Some direct Personal Hotspot navigation paths have changed in newer iOS versions.

⸻

VPN

prefs:root=General&path=VPN
App-prefs:root=General&path=VPN

⸻

Notifications

prefs:root=NOTIFICATIONS_ID
App-prefs:root=NOTIFICATIONS_ID

Scheduled Summary

prefs:root=NOTIFICATIONS_ID&path=SCHEDULED_SUMMARY

Notification Style

prefs:root=NOTIFICATIONS_ID&path=NOTIFICATION_STYLE

⸻

Sounds & Haptics

prefs:root=Sounds
App-prefs:root=Sounds

Ringtone

prefs:root=Sounds&path=Ringtone

Text Tone

prefs:root=Sounds&path=TextTone

⸻

Focus

prefs:root=DO_NOT_DISTURB
App-prefs:root=DO_NOT_DISTURB

⸻

Screen Time

prefs:root=SCREEN_TIME
App-prefs:root=SCREEN_TIME

⸻

General

prefs:root=General
App-prefs:root=General

About

prefs:root=General&path=About

Software Update

prefs:root=General&path=SOFTWARE_UPDATE_LINK

iPhone Storage

prefs:root=General&path=STORAGE_MGMT

Storage Management

prefs:root=General&path=STORAGE_MGMT

Offload Unused Apps

prefs:root=General&path=STORAGE_MGMT#OFFLOAD

AutoFill & Passwords

prefs:root=General&path=AUTOFILL

AutoFill Passwords

prefs:root=General&path=AUTOFILL#AUTOFILL

Verification Codes

prefs:root=General&path=AUTOFILL#SET_UP_VERIFICATION_CODES

Clean Up Verification Codes

prefs:root=General&path=AUTOFILL#CLEAN_UP_VERIFICATION_CODES

VPN & Device Management

prefs:root=General&path=ManagedConfigurationList

Dictionary

prefs:root=General&path=DICTIONARY

Language & Region

prefs:root=General&path=INTERNATIONAL

Region

prefs:root=General&path=INTERNATIONAL/LOCALE

Calendar

prefs:root=General&path=INTERNATIONAL/CALENDAR

Numbering System

prefs:root=General&path=INTERNATIONAL/NUMBERING_SYSTEM

Temperature Unit

prefs:root=General&path=INTERNATIONAL/TEMPERATURE_UNIT

Preferred Language

prefs:root=General&path=INTERNATIONAL#PREFERRED_LANGUAGE_GROUP

Add Language

prefs:root=General&path=INTERNATIONAL#ADD_PREFERRED_LANGUAGE

AirDrop

prefs:root=General&path=AIRDROP_LINK

Bringing Devices Together

prefs:root=General&path=AIRDROP_LINK#AIRDROP_NFC_ID

AirPlay & Continuity

prefs:root=General&path=CONTINUITY_SPEC

Handoff

prefs:root=General&path=CONTINUITY_SPEC#CONTINUITY

Transfer to HomePod

prefs:root=General&path=CONTINUITY_SPEC#TRANSFER_TO_HOMEPOD

Automatically AirPlay

prefs:root=General&path=CONTINUITY_SPEC#AUTOMATICALLY_AIRPLAY

Continuity Camera

prefs:root=General&path=CONTINUITY_SPEC#WOMBAT_CAMERA

CarPlay

prefs:root=General&path=CARPLAY

Date & Time

prefs:root=General&path=DATE_AND_TIME

Keyboard

prefs:root=General&path=Keyboard

Fonts

prefs:root=General&path=Fonts

Legal & Regulatory

prefs:root=General&path=LEGAL_AND_REGULATORY

AppleCare & Warranty

prefs:root=General&path=COVERAGE/

⸻

Accessibility

prefs:root=ACCESSIBILITY
App-prefs:root=ACCESSIBILITY

VoiceOver

prefs:root=ACCESSIBILITY&path=VOICEOVER

Zoom

prefs:root=ACCESSIBILITY&path=ZOOM

Display & Text Size

prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT

Motion

prefs:root=ACCESSIBILITY&path=MOTION

Spoken Content

prefs:root=ACCESSIBILITY&path=SPEECH

Touch

prefs:root=ACCESSIBILITY&path=TOUCH

Face ID & Attention

prefs:root=ACCESSIBILITY&path=FACE_ID

Switch Control

prefs:root=ACCESSIBILITY&path=SwitchControl

AssistiveTouch

prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY

Guided Access

prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS

⸻

Privacy & Security

Main page

Legacy:

prefs:root=Privacy

Modern navigation:

settings-navigation://com.apple.Settings.PrivacyAndSecurity

Location Services

prefs:root=Privacy&path=LOCATION
settings-navigation://com.apple.Settings.PrivacyAndSecurity/LOCATION

Location Sharing

prefs:root=Privacy&path=LOCATION/LOCATION_SHARING

Contacts

prefs:root=Privacy&path=CONTACTS
settings-navigation://com.apple.Settings.PrivacyAndSecurity/CONTACTS

Calendars

prefs:root=Privacy&path=CALENDARS

Photos

prefs:root=Privacy&path=PHOTOS
settings-navigation://com.apple.Settings.PrivacyAndSecurity/PHOTOS

Camera

prefs:root=Privacy&path=CAMERA
settings-navigation://com.apple.Settings.PrivacyAndSecurity/CAMERA

Microphone

prefs:root=Privacy&path=MICROPHONE
settings-navigation://com.apple.Settings.PrivacyAndSecurity/MICROPHONE

Bluetooth

prefs:root=Privacy&path=BT_PERIPHERAL
settings-navigation://com.apple.Settings.PrivacyAndSecurity/BT_PERIPHERAL

Speech Recognition

prefs:root=Privacy&path=SPEECH_RECOGNITION

Health

prefs:root=Privacy&path=HEALTH
settings-navigation://com.apple.Settings.PrivacyAndSecurity/HEALTH

Health Data

prefs:root=Privacy&path=HEALTH_DATA

HomeKit

prefs:root=Privacy&path=WILLOW

Media & Apple Music

prefs:root=Privacy&path=MEDIALIBRARY

Files & Folders

prefs:root=Privacy&path=FILEACCESS

Tracking

prefs:root=Privacy&path=USER_TRACKING
settings-navigation://com.apple.Settings.PrivacyAndSecurity/USER_TRACKING

Advertising

prefs:root=Privacy&path=ADVERTISING

Analytics & Improvements

prefs:root=Privacy&path=PROBLEM_REPORTING

App Privacy Report

prefs:root=Privacy&path=PRIVACY_REPORT

Lockdown Mode

prefs:root=Privacy#LOCKDOWN_MODE
settings-navigation://com.apple.Settings.PrivacyAndSecurity#LOCKDOWN_MODE

Sensitive Content Warning

prefs:root=Privacy#NUDITY_DETECTION

⸻

Battery

prefs:root=BATTERY_USAGE
App-prefs:root=BATTERY_USAGE

⸻

Display & Brightness

prefs:root=DISPLAY
App-prefs:root=DISPLAY

Auto-Lock

prefs:root=DISPLAY&path=AUTOLOCK

Text Size

prefs:root=DISPLAY&path=TEXT_SIZE

Display Zoom

prefs:root=DISPLAY&path=ZOOM

Dark Mode

prefs:root=DISPLAY#LockAppearance

True Tone

prefs:root=DISPLAY#TrueTone

Night Shift

prefs:root=DISPLAY&path=BLUE_LIGHT_REDUCTION

⸻

Wallpaper

prefs:root=Wallpaper

⚠️ iOS 18.1+

This destination has been reported to no longer navigate directly to
Wallpaper settings from some contexts.

Keep this URL for historical/reference purposes.

⸻

Siri

prefs:root=SIRI
App-prefs:root=SIRI

⸻

Face ID & Passcode

prefs:root=PASSCODE
App-prefs:root=PASSCODE

⸻

Emergency SOS

prefs:root=EmergencySOS
App-prefs:root=EmergencySOS

⸻

App Store

prefs:root=STORE
App-prefs:root=STORE

⸻

Wallet & Apple Pay

prefs:root=PASSBOOK
App-prefs:root=PASSBOOK

Apple Cash

prefs:root=PASSBOOK#Apple%C2%A0Cash

Payment Cards

prefs:root=PASSBOOK#SETTINGS_PAYMENT_CARDS_GROUP

Add Card

prefs:root=PASSBOOK#Add%20Card

Double-Click Side Button

prefs:root=PASSBOOK#Double-Click%20Side%20Button

Order Tracking

prefs:root=PASSBOOK#ORDER_TRACKING

⸻

Passwords

Modern iOS has a dedicated Passwords destination.

prefs:root=PASSWORDS
App-prefs:root=PASSWORDS

ℹ️ This replaces the role previously served by the older
Accounts & Passwords settings area.

⸻

Safari

prefs:root=SAFARI
App-prefs:root=SAFARI

Extensions

prefs:root=SAFARI&path=WEB_EXTENSIONS

Modern Settings navigation:

settings-navigation://com.apple.Settings.Apps/com.apple.mobilesafari/WEB_EXTENSIONS

For Safari Web Extensions, prefer Apple’s SFSafariSettings API when possible.

⸻

Mail

prefs:root=MAIL

Accounts

prefs:root=MAIL&path=ACCOUNTS

Add Account

prefs:root=MAIL&path=ACCOUNTS#ADD_ACCOUNT

Fetch New Data

prefs:root=MAIL&path=ACCOUNTS#FETCH_NEW_DATA

⸻

Messages

prefs:root=MESSAGES
App-prefs:root=MESSAGES

⸻

Phone

prefs:root=Phone
App-prefs:root=Phone

⸻

Contacts

prefs:root=CONTACTS
App-prefs:root=CONTACTS

⸻

Calendar

prefs:root=CALENDAR
App-prefs:root=CALENDAR

⸻

Notes

Notes

prefs:root=NOTES
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes

Default Account

prefs:root=NOTES&path=Default%20Account
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Default%20Account

Password

prefs:root=NOTES&path=Password
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Password

Sort Notes By

prefs:root=NOTES&path=Sort%20Notes%20By
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Sort%20Notes%20By

New Notes Start With

prefs:root=NOTES&path=New%20Notes%20Start%20With
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/New%20Notes%20Start%20With

Sort Checked Items

prefs:root=NOTES&path=Sort%20Checked%20Items
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Sort%20Checked%20Items

Lines & Grids

prefs:root=NOTES&path=Lines%20%26%20Grids
settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Lines%20%26%20Grids

Save to Photos

prefs:root=NOTES#Save%20to%20Photos

⸻

Photos

prefs:root=Photos
App-prefs:root=Photos

Transfer to Mac or PC

prefs:root=Photos#TransferGroup

⸻

Music

prefs:root=MUSIC
App-prefs:root=MUSIC

EQ

prefs:root=MUSIC&path=com.apple.Music%3AEQ

Sound Check

prefs:root=MUSIC#com.apple.Music%3ASoundCheck

Use Listening History

prefs:root=MUSIC#com.apple.Music%3APrivateListening

⸻

Podcasts

prefs:root=PODCASTS
App-prefs:root=PODCASTS

⸻

Maps

prefs:root=MAPS
App-prefs:root=MAPS

⸻

Health

prefs:root=HEALTH
App-prefs:root=HEALTH

⸻

Home

prefs:root=HOME
App-prefs:root=HOME

⸻

News

prefs:root=NEWS
App-prefs:root=NEWS

⸻

TV

prefs:root=TV
App-prefs:root=TV

⸻

Weather

prefs:root=WEATHER
App-prefs:root=WEATHER

⸻

Freeform

prefs:root=FREEFORM
App-prefs:root=FREEFORM

⸻

Journal

prefs:root=JOURNAL
App-prefs:root=JOURNAL

⸻

Developer

The Developer section is normally available after enabling Developer Mode.

prefs:root=DEVELOPER_SETTINGS
App-prefs:root=DEVELOPER_SETTINGS

Multipath Networking

prefs:root=DEVELOPER_SETTINGS&path=MULTI_PATH_AGG

Network Link Conditioner

prefs:root=DEVELOPER_SETTINGS&path=NLC

Logging

prefs:root=DEVELOPER_SETTINGS&path=DTInstrumentsSettings

Playable Content API

prefs:root=DEVELOPER_SETTINGS&path=RoutineSettings

TV Provider

prefs:root=DEVELOPER_SETTINGS&path=VideoSubscriberAccountSettings

ClassKit API

prefs:root=DEVELOPER_SETTINGS&path=ClassKitSettings

CoreSpotlight Testing

prefs:root=DEVELOPER_SETTINGS#CORESPOTLIGHT_TESTING

Shortcuts Testing

prefs:root=DEVELOPER_SETTINGS#SIRI_ACTIONS_TESTING

MIDI-CI Testing

prefs:root=DEVELOPER_SETTINGS#MIDI_CI_API_BETA

Hang Detection

prefs:root=DEVELOPER_SETTINGS#HANGTRACER_EXTERNAL_CONFIGURE

⸻

Legacy / Historical URLs

This repository intentionally keeps older URLs because they can still be useful for:

- older iOS versions
- research
- reverse engineering
- Shortcuts
- automation
- historical applications
- compatibility testing

Passwords & Accounts

Older iOS:

prefs:root=ACCOUNTS_AND_PASSWORDS
App-prefs:root=ACCOUNTS_AND_PASSWORDS

Modern iOS uses the dedicated PASSWORDS destination instead.

⸻

Restrictions

prefs:root=General&path=Restrictions

Older iOS versions used this destination. Modern iOS uses Screen Time for many of these controls.

⸻

Old Privacy naming

prefs:root=Privacy

Modern Settings displays this area as Privacy & Security.

⸻

Known Changes

Wallpaper

Older versions:

prefs:root=Wallpaper

Newer iOS releases may open the main Settings page rather than navigating directly to Wallpaper.

⸻

Wi-Fi

Older versions commonly supported:

prefs:root=WIFI

and:

App-prefs:root=WIFI

Behavior has become less reliable in newer iOS releases, particularly when opened programmatically by third-party apps.

⸻

Personal Hotspot

Older versions commonly used:

prefs:root=INTERNET_TETHERING

and:

App-prefs:root=INTERNET_TETHERING

Direct navigation behavior has changed in newer iOS releases.

⸻

Passwords

Older:

prefs:root=ACCOUNTS_AND_PASSWORDS

Modern:

prefs:root=PASSWORDS

⸻

Privacy

Older naming:

prefs:root=Privacy

Modern Settings UI:

Privacy & Security

Modern navigation may also use:

settings-navigation://com.apple.Settings.PrivacyAndSecurity

⸻

iOS 26+

iOS 26 introduced/expanded Settings navigation behavior using:

settings-navigation://

Examples:

Privacy & Security

settings-navigation://com.apple.Settings.PrivacyAndSecurity

Location

settings-navigation://com.apple.Settings.PrivacyAndSecurity/LOCATION

Microphone

settings-navigation://com.apple.Settings.PrivacyAndSecurity/MICROPHONE

Camera

settings-navigation://com.apple.Settings.PrivacyAndSecurity/CAMERA

Photos

settings-navigation://com.apple.Settings.PrivacyAndSecurity/PHOTOS

Bluetooth

settings-navigation://com.apple.Settings.PrivacyAndSecurity/BT_PERIPHERAL

Tracking

settings-navigation://com.apple.Settings.PrivacyAndSecurity/USER_TRACKING

Lockdown Mode

settings-navigation://com.apple.Settings.PrivacyAndSecurity#LOCKDOWN_MODE

Apple Account → Password & Security

settings-navigation://com.apple.Settings.AppleAccount/PASSWORD_AND_SECURITY

Apple Account → Payment & Shipping

settings-navigation://com.apple.Settings.AppleAccount/PAYMENT_AND_SHIPPING

Apple Account → Subscriptions

settings-navigation://com.apple.Settings.AppleAccount/SUBSCRIPTIONS

Notes

settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes

⸻

iOS 27

Status: ongoing compatibility testing

iOS 27 is a newer major iOS release and undocumented Settings URLs may change
without notice.

This repository should not claim that an undocumented URL works on iOS 27
unless it has been individually verified.

When reporting an iOS 27 result, include:

Device:
iOS version:
URL:
Opened from:
Result:
Expected result:

Example:

Device: iPhone 17 Pro
iOS: 27.0
URL: prefs:root=WIFI
Opened from: Shortcuts
Result: Settings opened
Expected: Wi-Fi page

⸻

Testing

If you are testing these URLs, test them separately from:

1. Shortcuts
2. Safari
3. A native iOS application
4. Xcode Simulator
5. A physical iPhone

These environments may behave differently.

For application testing:

if let url = URL(string: "prefs:root=WIFI") {
UIApplication.shared.open(url)
}

Do not assume that success means the URL is officially supported.

⸻

URL Encoding

Settings URLs frequently contain characters that must be percent encoded.

For example:

&

may appear inside a path as:

%26

A space:

becomes:

%20

A colon:

:

can become:

%3A

Example:

prefs:root=MUSIC&path=com.apple.Music%3AEQ

When adding new URLs, preserve the encoding used by the tested URL.

⸻

How to Open a URL

Swift

import UIKit
let urlString = "prefs:root=WIFI"
if let url = URL(string: urlString) {
UIApplication.shared.open(url)
}

Again, prefs: and App-prefs: are undocumented and should not be treated as public APIs.

⸻

Contributing

If you discover a new Settings URL or verify an existing one, please provide:

iOS version:
Device:
Settings destination:
URL:
How it was opened:
Result:

Example:

iOS version: 27.0
Device: iPhone
Destination: Privacy & Security → Microphone
URL: settings-navigation://com.apple.Settings.PrivacyAndSecurity/MICROPHONE
Opened from: Shortcuts
Result: Opened successfully

Please do not report a URL as universally working based on a single device or iOS version.

⸻

Sources & References

This repository is a community-maintained collection and is not affiliated with Apple.

Useful references include:

- Apple Developer Documentation
- Apple Developer Forums
- iOS Settings reverse-engineering research
- Community testing
- Previous versions of this repository
- Community-maintained iOS Settings URL databases

⸻

Disclaimer

This project is not affiliated with Apple Inc.

prefs:, App-prefs: and settings-navigation:// destinations documented here are generally undocumented/private implementation details unless explicitly stated otherwise.

Apple may remove, rename, relocate, or change these destinations at any time.

Use them at your own risk.

⸻
@1mehdifaraji

License

MIT

⸻

# Expanded URL Reference Ledger

This section is intentionally verbose. It is a machine-friendly and human-readable
index of URL strings preserved or observed by this project. It does not imply
that every entry is currently functional, public, or App Store-safe.

For current iOS 26-era routes, this README distinguishes documented Apple APIs
from undocumented Settings destinations. A community-maintained iOS 26.2 catalog
was used as an additional cross-reference for current route names and examples.

## Status vocabulary

- **Undocumented** — not a public Apple URL API.
- **Legacy** — retained for historical/compatibility research.
- **Current cross-reference** — present in the referenced iOS 26.2 community catalog.
- **Requires verification** — behavior should be tested on the exact iOS/device/context.
- **Documented API** — use Apple's public API when the task is opening your own app's settings.

## Important interpretation rule

A URL appearing in this README means only that the string is part of the project's
reference dataset. It is not a promise that Settings will honor the destination.

### 001. `Settings` — `prefs:`

**URL:** `prefs:root=WIFI`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 002. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=WIFI`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 003. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 004. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 005. `Apple Account / iCloud` — `App-prefs:`

**URL:** `App-prefs:root=APPLE_ACCOUNT`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 006. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=PASSWORD_AND_SECURITY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 007. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/PASSWORD_AND_SECURITY`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 008. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=PAYMENT_AND_SHIPPING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 009. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/PAYMENT_AND_SHIPPING`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 010. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=SUBSCRIPTIONS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 011. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/SUBSCRIPTIONS`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 012. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 013. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/STORAGE_AND_BACKUP`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 014. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=APPLE_ACCOUNT_CONTACT`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 015. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=LOCATION_SHARING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 016. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=Family`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 017. `Settings` — `prefs:`

**URL:** `prefs:root=AIRPLANE_MODE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 018. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=AIRPLANE_MODE`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 019. `Settings` — `prefs:`

**URL:** `prefs:root=Bluetooth`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 020. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=Bluetooth`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 021. `Settings` — `prefs:`

**URL:** `prefs:root=MOBILE_DATA_SETTINGS_ID`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 022. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=MOBILE_DATA_SETTINGS_ID`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 023. `Settings` — `prefs:`

**URL:** `prefs:root=INTERNET_TETHERING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 024. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=INTERNET_TETHERING`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 025. `General` — `prefs:`

**URL:** `prefs:root=General&path=VPN`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 026. `General` — `App-prefs:`

**URL:** `App-prefs:root=General&path=VPN`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 027. `Settings` — `prefs:`

**URL:** `prefs:root=NOTIFICATIONS_ID`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 028. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=NOTIFICATIONS_ID`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 029. `Settings` — `prefs:`

**URL:** `prefs:root=NOTIFICATIONS_ID&path=SCHEDULED_SUMMARY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 030. `Settings` — `prefs:`

**URL:** `prefs:root=NOTIFICATIONS_ID&path=NOTIFICATION_STYLE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 031. `Settings` — `prefs:`

**URL:** `prefs:root=Sounds`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 032. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=Sounds`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 033. `Settings` — `prefs:`

**URL:** `prefs:root=Sounds&path=Ringtone`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 034. `Settings` — `prefs:`

**URL:** `prefs:root=Sounds&path=TextTone`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 035. `Settings` — `prefs:`

**URL:** `prefs:root=DO_NOT_DISTURB`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 036. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=DO_NOT_DISTURB`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 037. `Settings` — `prefs:`

**URL:** `prefs:root=SCREEN_TIME`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 038. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=SCREEN_TIME`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 039. `General` — `prefs:`

**URL:** `prefs:root=General`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 040. `General` — `App-prefs:`

**URL:** `App-prefs:root=General`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 041. `General` — `prefs:`

**URL:** `prefs:root=General&path=About`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 042. `General` — `prefs:`

**URL:** `prefs:root=General&path=SOFTWARE_UPDATE_LINK`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 043. `General` — `prefs:`

**URL:** `prefs:root=General&path=STORAGE_MGMT`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 044. `General` — `prefs:`

**URL:** `prefs:root=General&path=STORAGE_MGMT#OFFLOAD`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 045. `General` — `prefs:`

**URL:** `prefs:root=General&path=AUTOFILL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 046. `General` — `prefs:`

**URL:** `prefs:root=General&path=AUTOFILL#AUTOFILL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 047. `General` — `prefs:`

**URL:** `prefs:root=General&path=AUTOFILL#SET_UP_VERIFICATION_CODES`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 048. `General` — `prefs:`

**URL:** `prefs:root=General&path=AUTOFILL#CLEAN_UP_VERIFICATION_CODES`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 049. `General` — `prefs:`

**URL:** `prefs:root=General&path=ManagedConfigurationList`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 050. `General` — `prefs:`

**URL:** `prefs:root=General&path=DICTIONARY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 051. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 052. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL/LOCALE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 053. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL/CALENDAR`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 054. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL/NUMBERING_SYSTEM`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 055. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL/TEMPERATURE_UNIT`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 056. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL#PREFERRED_LANGUAGE_GROUP`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 057. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL#ADD_PREFERRED_LANGUAGE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 058. `General` — `prefs:`

**URL:** `prefs:root=General&path=AIRDROP_LINK`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 059. `General` — `prefs:`

**URL:** `prefs:root=General&path=AIRDROP_LINK#AIRDROP_NFC_ID`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 060. `General` — `prefs:`

**URL:** `prefs:root=General&path=CONTINUITY_SPEC`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 061. `General` — `prefs:`

**URL:** `prefs:root=General&path=CONTINUITY_SPEC#CONTINUITY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 062. `General` — `prefs:`

**URL:** `prefs:root=General&path=CONTINUITY_SPEC#TRANSFER_TO_HOMEPOD`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 063. `General` — `prefs:`

**URL:** `prefs:root=General&path=CONTINUITY_SPEC#AUTOMATICALLY_AIRPLAY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 064. `General` — `prefs:`

**URL:** `prefs:root=General&path=CONTINUITY_SPEC#WOMBAT_CAMERA`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 065. `General` — `prefs:`

**URL:** `prefs:root=General&path=CARPLAY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 066. `General` — `prefs:`

**URL:** `prefs:root=General&path=DATE_AND_TIME`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 067. `General` — `prefs:`

**URL:** `prefs:root=General&path=Keyboard`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 068. `General` — `prefs:`

**URL:** `prefs:root=General&path=Fonts`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 069. `General` — `prefs:`

**URL:** `prefs:root=General&path=LEGAL_AND_REGULATORY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 070. `General` — `prefs:`

**URL:** `prefs:root=General&path=COVERAGE/`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 071. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 072. `Accessibility` — `App-prefs:`

**URL:** `App-prefs:root=ACCESSIBILITY`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 073. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=VOICEOVER`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 074. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=ZOOM`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 075. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 076. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=MOTION`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 077. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=SPEECH`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 078. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=TOUCH`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 079. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=FACE_ID`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 080. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=SwitchControl`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 081. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 082. `Accessibility` — `prefs:`

**URL:** `prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 083. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 084. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=LOCATION`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 085. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/LOCATION`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 086. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=LOCATION/LOCATION_SHARING`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 087. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=CONTACTS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 088. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/CONTACTS`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 089. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=CALENDARS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 090. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=PHOTOS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 091. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/PHOTOS`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 092. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=CAMERA`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 093. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/CAMERA`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 094. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=MICROPHONE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 095. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/MICROPHONE`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 096. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=BT_PERIPHERAL`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 097. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/BT_PERIPHERAL`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 098. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=SPEECH_RECOGNITION`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 099. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=HEALTH`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 100. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/HEALTH`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 101. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=HEALTH_DATA`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 102. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=WILLOW`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 103. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=MEDIALIBRARY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 104. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=FILEACCESS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 105. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=USER_TRACKING`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 106. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/USER_TRACKING`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 107. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=ADVERTISING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 108. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=PROBLEM_REPORTING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 109. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=PRIVACY_REPORT`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 110. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy#LOCKDOWN_MODE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 111. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity#LOCKDOWN_MODE`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 112. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy#NUDITY_DETECTION`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 113. `Settings` — `prefs:`

**URL:** `prefs:root=BATTERY_USAGE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 114. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=BATTERY_USAGE`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 115. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 116. `Display & Brightness` — `App-prefs:`

**URL:** `App-prefs:root=DISPLAY`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 117. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=AUTOLOCK`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 118. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=TEXT_SIZE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 119. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=ZOOM`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 120. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY#LockAppearance`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 121. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY#TrueTone`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 122. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=BLUE_LIGHT_REDUCTION`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 123. `Settings` — `prefs:`

**URL:** `prefs:root=Wallpaper`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 124. `Siri` — `prefs:`

**URL:** `prefs:root=SIRI`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 125. `Siri` — `App-prefs:`

**URL:** `App-prefs:root=SIRI`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 126. `Settings` — `prefs:`

**URL:** `prefs:root=PASSCODE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 127. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=PASSCODE`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 128. `Settings` — `prefs:`

**URL:** `prefs:root=EmergencySOS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 129. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=EmergencySOS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 130. `App Store` — `prefs:`

**URL:** `prefs:root=STORE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 131. `App Store` — `App-prefs:`

**URL:** `App-prefs:root=STORE`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 132. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 133. `Wallet & Apple Pay` — `App-prefs:`

**URL:** `App-prefs:root=PASSBOOK`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 134. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK#Apple%C2%A0Cash`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 135. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK#SETTINGS_PAYMENT_CARDS_GROUP`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 136. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK#Add%20Card`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 137. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK#Double-Click%20Side%20Button`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 138. `Wallet & Apple Pay` — `prefs:`

**URL:** `prefs:root=PASSBOOK#ORDER_TRACKING`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 139. `Settings` — `prefs:`

**URL:** `prefs:root=PASSWORDS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 140. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=PASSWORDS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 141. `Settings` — `prefs:`

**URL:** `prefs:root=SAFARI`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 142. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=SAFARI`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 143. `Settings` — `prefs:`

**URL:** `prefs:root=SAFARI&path=WEB_EXTENSIONS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 144. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilesafari/WEB_EXTENSIONS`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 145. `Settings` — `prefs:`

**URL:** `prefs:root=MAIL`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 146. `Settings` — `prefs:`

**URL:** `prefs:root=MAIL&path=ACCOUNTS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 147. `Settings` — `prefs:`

**URL:** `prefs:root=MAIL&path=ACCOUNTS#ADD_ACCOUNT`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 148. `Settings` — `prefs:`

**URL:** `prefs:root=MAIL&path=ACCOUNTS#FETCH_NEW_DATA`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 149. `Settings` — `prefs:`

**URL:** `prefs:root=MESSAGES`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 150. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=MESSAGES`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 151. `Settings` — `prefs:`

**URL:** `prefs:root=Phone`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 152. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=Phone`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 153. `Settings` — `prefs:`

**URL:** `prefs:root=CONTACTS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 154. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=CONTACTS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 155. `Settings` — `prefs:`

**URL:** `prefs:root=CALENDAR`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 156. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=CALENDAR`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 157. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 158. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 159. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=Default%20Account`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 160. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Default%20Account`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 161. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=Password`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 162. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Password`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 163. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=Sort%20Notes%20By`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 164. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Sort%20Notes%20By`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 165. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=New%20Notes%20Start%20With`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 166. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/New%20Notes%20Start%20With`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 167. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=Sort%20Checked%20Items`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 168. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Sort%20Checked%20Items`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 169. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES&path=Lines%20%26%20Grids`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 170. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.mobilenotes/Lines%20%26%20Grids`
**Scheme:** `settings-navigation://`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 171. `Notes` — `prefs:`

**URL:** `prefs:root=NOTES#Save%20to%20Photos`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 172. `Settings` — `prefs:`

**URL:** `prefs:root=Photos`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 173. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=Photos`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 174. `Settings` — `prefs:`

**URL:** `prefs:root=Photos#TransferGroup`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 175. `Music` — `prefs:`

**URL:** `prefs:root=MUSIC`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 176. `Music` — `App-prefs:`

**URL:** `App-prefs:root=MUSIC`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 177. `Music` — `prefs:`

**URL:** `prefs:root=MUSIC&path=com.apple.Music%3AEQ`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 178. `Music` — `prefs:`

**URL:** `prefs:root=MUSIC#com.apple.Music%3ASoundCheck`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 179. `Music` — `prefs:`

**URL:** `prefs:root=MUSIC#com.apple.Music%3APrivateListening`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 180. `Settings` — `prefs:`

**URL:** `prefs:root=PODCASTS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 181. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=PODCASTS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 182. `Settings` — `prefs:`

**URL:** `prefs:root=MAPS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 183. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=MAPS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 184. `Settings` — `prefs:`

**URL:** `prefs:root=HEALTH`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 185. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=HEALTH`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 186. `Settings` — `prefs:`

**URL:** `prefs:root=HOME`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 187. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=HOME`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 188. `Settings` — `prefs:`

**URL:** `prefs:root=NEWS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 189. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=NEWS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 190. `Settings` — `prefs:`

**URL:** `prefs:root=TV`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 191. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=TV`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 192. `Settings` — `prefs:`

**URL:** `prefs:root=WEATHER`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 193. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=WEATHER`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 194. `Settings` — `prefs:`

**URL:** `prefs:root=FREEFORM`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 195. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=FREEFORM`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 196. `Settings` — `prefs:`

**URL:** `prefs:root=JOURNAL`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 197. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=JOURNAL`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 198. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 199. `Developer` — `App-prefs:`

**URL:** `App-prefs:root=DEVELOPER_SETTINGS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 200. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=MULTI_PATH_AGG`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 201. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=NLC`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 202. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=DTInstrumentsSettings`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 203. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=RoutineSettings`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 204. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=VideoSubscriberAccountSettings`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 205. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS&path=ClassKitSettings`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 206. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS#CORESPOTLIGHT_TESTING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 207. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS#SIRI_ACTIONS_TESTING`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 208. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS#MIDI_CI_API_BETA`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 209. `Developer` — `prefs:`

**URL:** `prefs:root=DEVELOPER_SETTINGS#HANGTRACER_EXTERNAL_CONFIGURE`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 210. `Settings` — `prefs:`

**URL:** `prefs:root=ACCOUNTS_AND_PASSWORDS`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 211. `Settings` — `App-prefs:`

**URL:** `App-prefs:root=ACCOUNTS_AND_PASSWORDS`
**Scheme:** `App-prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 212. `General` — `prefs:`

**URL:** `prefs:root=General&path=Restrictions`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 213. `Settings` — `prefs:`

**URL:** `prefs:root=WIFI"`
**Scheme:** `prefs:`
**Status:** Preserved reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 214. `Settings` — `prefs:`

**URL:** `prefs:root=BATTERY_USAGE#BATTERY_SAVER_MODE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 215. `Settings` — `prefs:`

**URL:** `prefs:root=BATTERY_USAGE#BATTERY_HEALTH_ID`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 216. `General` — `prefs:`

**URL:** `prefs:root=General&path=Keyboard/KEYBOARDS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 217. `General` — `prefs:`

**URL:** `prefs:root=General&path=SOFTWARE_UPDATE_LINK/SUAutomaticUpdateButton`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 218. `General` — `prefs:`

**URL:** `prefs:root=General&path=STORAGE_MGMT#MANAGE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 219. `General` — `prefs:`

**URL:** `prefs:root=General&path=PiP_SPEC`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 220. `General` — `prefs:`

**URL:** `prefs:root=General&path=POINTERS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 221. `General` — `prefs:`

**URL:** `prefs:root=General&path=NFC_LINK`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 222. `General` — `prefs:`

**URL:** `prefs:root=General&path=About/CERT_TRUST_SETTINGS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 223. `General` — `prefs:`

**URL:** `prefs:root=General&path=About#SerialNumber`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 224. `General` — `prefs:`

**URL:** `prefs:root=General&path=About#ProductModel`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 225. `General` — `prefs:`

**URL:** `prefs:root=General&path=About#ProductModelName`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 226. `General` — `prefs:`

**URL:** `prefs:root=General&path=About/SW_VERSION_SPECIFIER`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 227. `General` — `prefs:`

**URL:** `prefs:root=General&path=LEGAL_AND_REGULATORY#Warranty`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 228. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 229. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#settingsErase`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 230. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#fullErase`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 231. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#RESET_NETWORK_LABEL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 232. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#cellularErase`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 233. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#SUBSCRIBER_SERVICES_ID`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 234. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#RESET_KEYBOARD_DICTIONARY_LABEL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 235. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#RESET_ICONS_LABEL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 236. `General` — `prefs:`

**URL:** `prefs:root=General&path=Reset#RESET_PRIVACY_LABEL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 237. `General` — `prefs:`

**URL:** `prefs:root=General#SHUTDOWN_LABEL`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 238. `General` — `prefs:`

**URL:** `prefs:root=General&path=INTERNATIONAL#NEW_PREFERRED_LANGUAGE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 239. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 240. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=TRANSPARENCY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 241. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/TRANSPARENCY`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 242. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 243. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/STORAGE_AND_BACKUP`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 244. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Ubiquity`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 245. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Ubiquity`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 246. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.MediaStream`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 247. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.MediaStream`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 248. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Mail`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 249. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Mail`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 250. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Contacts`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 251. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Contacts`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 252. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Calendars`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 253. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Calendars`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 254. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Reminders`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 255. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Reminders`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 256. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Bookmarks`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 257. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Bookmarks`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 258. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Notes`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 259. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Notes`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 260. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.News`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 261. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.News`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 262. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/BACKUP`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 263. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/BACKUP`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 264. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.Health`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 265. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.Health`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 266. `Apple Account / iCloud` — `prefs:`

**URL:** `prefs:root=APPLE_ACCOUNT&path=ICLOUD_SERVICE/com.apple.Dataclass.KeychainSync`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 267. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/ICLOUD_SERVICE/com.apple.Dataclass.KeychainSync`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 268. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.AppleAccount/Family`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 269. `Settings` — `prefs:`

**URL:** `prefs:root=NOTIFICATIONS_ID&path=SCHEDULED_DELIVERY_ID`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 270. `Settings` — `prefs:`

**URL:** `prefs:root=DO_NOT_DISTURB&path=status`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 271. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY#DEVICE_APPEARANCE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 272. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY#WHITE_BALANCE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 273. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=BLUE_LIGHT_REDUCTION#SCHEDULED`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 274. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=APPEARANCE#TWO_HANDED_WINDOW_ZOOM`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 275. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=MAGNIFY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 276. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=ALWAYS_ON`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 277. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=ALWAYS_ON#ALWAYS_ON`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 278. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=COMPATIBLE_APPEARANCE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 279. `Display & Brightness` — `prefs:`

**URL:** `prefs:root=DISPLAY&path=COMPATIBLE_APPEARANCE#COMPATIBLE_APPEARANCE_CHOICES`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 280. `Measure` — `prefs:`

**URL:** `prefs:root=MEASURE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 281. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.measure`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 282. `Measure` — `prefs:`

**URL:** `prefs:root=MEASURE#MEASURE_UNITS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 283. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.measure#MEASURE_UNITS#MEASURE_UNITS`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 284. `Measure` — `prefs:`

**URL:** `prefs:root=MEASURE#Imperial`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 285. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.measure#Imperial#Imperial`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 286. `Measure` — `prefs:`

**URL:** `prefs:root=MEASURE#Metric`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 287. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.Apps/com.apple.measure#Metric#Metric`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 288. `Settings` — `prefs:`

**URL:** `prefs:root=ControlCenter`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 289. `Settings` — `prefs:`

**URL:** `prefs:root=ControlCenter#ALLOWED_WITHIN_APPS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 290. `Settings` — `prefs:`

**URL:** `prefs:root=ControlCenter&path=CUSTOMIZE_CONTROLS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 291. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#READING`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 292. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKFullJustification`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 293. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKAutoHyphenation`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 294. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKLeftTapTurnToNext`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 295. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#READING_GOALS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 296. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKReadingGoalsShouldClearDataKey`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 297. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#SEARCHING`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 298. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKIncludeBookStoreResultsInSearch`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 299. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#AUDIOBOOKS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 300. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS&path=BKAudioBookSkipForward`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 301. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS&path=BKAudioBookSkipBackward`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 302. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BKRemoteSkipInsteadOfNextTrackDefaultKey`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 303. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#Next/Previous`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 304. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#Skip%20Forward/Back`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 305. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#PRIVACY`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 306. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS#BAResetAnalyticsUserID`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 307. `Books` — `prefs:`

**URL:** `prefs:root=IBOOKS&path=Acknowledgements`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 308. `Camera` — `prefs:`

**URL:** `prefs:root=CAMERA&path=CameraFormatsSettingsList#CAMUserPreferenceEnableLinearDNGControl`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 309. `Camera` — `prefs:`

**URL:** `prefs:root=CAMERA&path=Record%20Video#HDR%20Video`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 310. `Settings` — `prefs:`

**URL:** `prefs:root=COMPASS#USE_TRUE_NORTH`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 311. `Privacy & Security` — `prefs:`

**URL:** `prefs:root=Privacy&path=REMINDERS`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 312. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/REMINDERS`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 313. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/SPEECH_RECOGNITION`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 314. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/WILLOW`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 315. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/MEDIALIBRARY`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 316. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/PROBLEM_REPORTING`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 317. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/ADVERTISING`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 318. `Settings` — `settings-navigation://`

**URL:** `settings-navigation://com.apple.Settings.PrivacyAndSecurity/FILEACCESS`
**Scheme:** `settings-navigation://`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private destination; verify on the target iOS release.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 319. `Settings` — `prefs:`

**URL:** `prefs:root=Sounds&path=Personalized%20Spatial%20Audio`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 320. `Settings` — `prefs:`

**URL:** `prefs:root=Pencil`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 321. `Settings` — `prefs:`

**URL:** `prefs:root=Pencil#PrefersPencilDraws`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 322. `Settings` — `prefs:`

**URL:** `prefs:root=Pencil#PencilTextInput`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 323. `Settings` — `prefs:`

**URL:** `prefs:root=TRANSLATE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 324. `Settings` — `prefs:`

**URL:** `prefs:root=TRANSLATE#OnDeviceOnly`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 325. `App Store` — `prefs:`

**URL:** `prefs:root=STORE#Automatic%20Downloads`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 326. `App Store` — `prefs:`

**URL:** `prefs:root=STORE#App%20Updates`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 327. `App Store` — `prefs:`

**URL:** `prefs:root=STORE&path=App%20Downloads`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 328. `App Store` — `prefs:`

**URL:** `prefs:root=STORE&path=Video%20Autoplay`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 329. `App Store` — `prefs:`

**URL:** `prefs:root=STORE#In-App%20Ratings%20&%20Reviews`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

### 330. `Settings` — `prefs:`

**URL:** `prefs:root=ROOT#AIRPLANE_MODE`
**Scheme:** `prefs:`
**Status:** Current cross-reference; requires verification
**Risk:** Undocumented/private Settings URL; behavior can change between releases.
**Testing note:** Test from Shortcuts, Safari, a native app, and a physical device separately; record iOS version, device, source context, and observed destination.

⸻

## Public API guidance

For an App Store application, prefer Apple's documented APIs whenever the destination
is the application's own Settings page or its notification settings.

### Application Settings

```swift
import UIKit

if let url = URL(string: UIApplication.openSettingsURLString) {
    await UIApplication.shared.open(url)
}
```

Apple documents `UIApplication.openSettingsURLString` as the URL string used to
deep-link to an app's custom Settings page. This is different from private
`prefs:` routes because it is an Apple-provided API.

### Application Notification Settings

```swift
import UIKit

if let url = URL(string: UIApplication.openNotificationSettingsURLString) {
    await UIApplication.shared.open(url)
}
```

Apple documents `UIApplication.openNotificationSettingsURLString` for deep-linking
to an application's notification settings.

### Default Applications Settings

Apple's current UIKit documentation lists `openDefaultApplicationsSettingsURLString`
as deprecated. Treat it as a compatibility reference rather than a recommendation
for new code.

## Current iOS 26.2 cross-reference

A maintained community catalog for iOS 26.2 currently lists 414 lines of
`prefs:` destinations. This README intentionally does not convert those community
entries into claims of Apple support. Examples include Battery Health, AutoFill,
Software Update automatic updates, Apple Account/iCloud sub-destinations,
Display & Brightness, Wallet, Developer settings, Books, Camera, Privacy & Security,
Translate, Siri, and App Store destinations.

## iOS 27 verification policy

The repository may contain an iOS 27 testing section because this project is updated
during an evolving OS cycle. Do not label an undocumented URL as "working on iOS 27"
unless the result has actually been reproduced on a specified iOS 27 build/device.

When reporting a result, include:

- iOS version/build
- device model
- URL
- scheme
- where it was opened from
- expected destination
- actual destination
- whether Settings opened
- whether the URL merely opened the Settings root
- whether behavior differed between simulator and physical hardware

## Reproducible test record

```text
iOS version/build:
Device:
URL:
Scheme:
Opened from:
Expected:
Actual:
Settings opened:
Direct destination:
Notes:
```

## Pull request checklist

Before adding a URL:

- Confirm the URL is syntactically valid.
- Record the exact iOS version/build.
- Record the device model.
- Test the exact URL rather than a visually similar variant.
- Record whether the test was from Shortcuts, Safari, or an application.
- Record whether the destination opened directly or only opened Settings.
- Preserve percent encoding.
- Do not describe a private route as an Apple-supported public API.
- Keep older routes when they have historical value.
- Prefer a documented Apple API when one exists.
- Avoid claiming universal compatibility from one successful test.
- Add a source or reproducible observation when possible.

## License

MIT

## Developer

[@1mehdifaraji](https://github.com/1mehdifaraji)
