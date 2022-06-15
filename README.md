# Social App

In-progress social app.

Uses:

- [React Native](https://reactnative.dev)
- [React Native for Web](https://necolas.github.io/react-native-web/)
- [React Navigation](https://reactnative.dev/docs/navigation#react-navigation)
- [MobX](https://mobx.js.org/README.html) and [MobX State Tree](https://mobx-state-tree.js.org/)
- [Async Storage](https://github.com/react-native-async-storage/async-storage)

## Build instructions

- Setup your environment [using the react native instructions](https://reactnative.dev/docs/environment-setup).
- After initial setup:
  - `cd ios ; pod install`
- Start the dev servers
  - `yarn dev-pds`
  - `yarn dev-wallet`
- Run the dev app
  - iOS: `yarn ios`
  - Android: `yarn android`
  - Web: `yarn web`
- Tips
  - `npx react-native info` Checks what has been installed.
  - On M1 macs, you need to exclude "arm64" from the target architectures
    - Annoyingly this must be re-set via XCode after every pod install

## Various notes

- ["SSO" flows on mobile](https://developer.okta.com/blog/2022/01/13/mobile-sso)
  - Suggests we might want to use `ASWebAuthenticationSession` on iOS
  - [react-native-inappbrowser-reborn](https://www.npmjs.com/package/react-native-inappbrowser-reborn) with `openAuth: true` might be worth exploring
  - We might even [get rejected by the app store](https://community.auth0.com/t/react-native-ios-app-rejected-on-appstore-for-using-react-native-auth0/36793) if we don't
- Cryptography
  - We rely on [isomorphic-webcrypto](https://github.com/kevlened/isomorphic-webcrypto)
  - For the CRNG this uses [react-native-securerandom](https://github.com/robhogan/react-native-securerandom) which provides proper random on mobile
  - For the crypto this uses [msrcrypto](https://github.com/kevlened/msrCrypto) - but we should consider switching to [the MS maintained version](https://github.com/microsoft/MSR-JavaScript-Crypto)
  - In the future it might be preferable to move off of msrcrypto and use iOS and Android native modules, but nothing is available right now