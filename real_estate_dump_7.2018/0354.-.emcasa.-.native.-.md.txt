# Real Estate Mobile Client

## Install

1. Clone this repository

```sh
git clone https://github.com/em-casa/native.git
cd native
```

2. Install dev dependencies

```sh
yarn install
bundle install
(cd ios && pod install)
```

## Run

To run and develop the app locally:

1. Start the bundler: `yarn start`
2. Run a simulator: `yarn ios` or `yarn android`

In development mode, this app communicates with the staging API server `https://em-casa-backend-staging.herokuapp.com` by default.
Optionally, to use a local instance of the backend server:

3. Download and run [em-casa/backend](https://github.com/em-casa/backend)
4. `export API_CLIENT="https://localhost:4000"`
5. Restart the bundler

## Build

### Android

```sh
bundle exec fastlane android build
```

The android `apk` distributable is outputted into `android/app/build/outputs/apk/`.

You can pass any of the following options to fastlane's build task by appending `{option}:{value}` to the command.

e.g: `bundle exec fastlane android build bump:true version:1.0.0`

| option       |   type   |        default         | description                 |
| ------------ | :------: | :--------------------: | --------------------------- |
| signed\*     |  `bool`  |        `false`         | Enable code signing         |
| bump         |  `bool`  |        `false`         | Bump version number         |
| build_number |  `int`   | current build n˚ + `1` | New build number to bump to |
| version      | `string` | package.json `version` | New version to bump to      |

\* Requires the `ANDROID_KEY*` environment variables. See [.env.example](.env.example)

### IOS

TODO

## Release

This project uses Crashnalytics for beta testing.

### Android

```sh
bundle exec fastlane android beta
```

In addition to all of `build` task's options, you can pass the following to `beta`:

| option  |   type   | default | description                                                          |
| ------- | :------: | :-----: | -------------------------------------------------------------------- |
| groups  | `string` |  `nil`  | Comma delimited list of beta tester groups to invite for this update |
| promote |  `bool`  | `false` | Send update notifications to beta testers                            |
| comment | `string` |  `nil`  | Release notes                                                        |

## IOS

TODO

## Contribute

Feel free to open issues and PRs.

At the moment, we're tracking tasks at https://www.pivotaltracker.com/n/projects/2125081

---

This project was bootstrapped with [Create React Native App](https://github.com/react-community/create-react-native-app).
