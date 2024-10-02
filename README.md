# Rewarded Interests’s On-page Advertising Token Access API

**Version** 1.0

**Date**: October 2024

**Audience**: Public (DSP partners, header bidding implementers, other ad tech community)

**Access**: Internal, Engineering Partners, and Ad Tech Partners

### Summary / Background

This document describes and provides usage instructions for Rewarded Interest’s Javascript API that provides advertising identifier tokens to on-page parties on behalf of consumers.

### Glossary of Terms

**Rewarded Interest Advertising Token**: an opaque string which can be resolved into a Rewarded Interest Advertising ID.

**Rewarded Interest Advertising ID aka CMAID**: A durable, cross-site, cross-device advertising identifier. This ID remains consistent across visits and across a Rewarded Interest user’s various enrolled devices, unless they reset or pause it.

**CMAID**: An acronym for Consumer Mediated Advertising Identifier

### Usage

Suppose you are implementing a header-bidding ID module. You wish to fetch the Rewarded Interest Advertising Token to supply it into the bid-stream to allow DSP to bid with knowledge of the identity. Here’s what you’d do:

1. Retrieve the token from our API

```typescript
const riToken: string = await window.__riApi.getAdvertisingToken();
```

2. Use the token for the remainder of the page session, i.e. until the user leaves the current page

### API reference

This object is available glocally as `window.__riApi`

```typescript
interface RewardedInterestBrowserPartnerApi {
  /*
   * Retrieves the Rewarded Interest API version.
   * Note: Api version is a string in the format of "major.minor.patch".
   * @returns string.
   */
  getApiVersion(): string;

  /**
   * Retrieves the current advertising token.
   * Note: Successive calls to this method may return different tokens.
   * @usage Call this method exactly one per page. DO NOT STORE THIS TOKEN.
   * @returns string.
   */
  getAdvertisingToken(): Promise<string>;
}
```

### FAQ

Q. When will the `window.__riApi` object become available?

A. By the time the `window` `load` event is fired

---

Q. In what case will the `window.__riApi` object not be available

A. If the user is not using our plugin _or_ has not yet accepted our terms of service.

---

Q. How is consent managed for these IDs

A. The availability of the API is subject to our user’s general or site-specific consent policy, as known to our extension.

---

Q. How and why would a Rewarded Interest Advertising ID be reset?

A. At any time if a user wants to no longer see ads relevant to their browsing history (maybe a friend was using their computer), they can reset the ID from their users settings.

---

Q. How and why would a Rewarded Interest Advertising ID be paused?

A. At any time if a user wants to stop seeing ads targeted through Rewarded Interest but does not wish to close their account, they can pause their ID from their use settings.