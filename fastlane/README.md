# Fastlane Documentation

## Installation

```bash
# Install fastlane
gem install fastlane
```

## Available Actions

### Android

#### android test
```bash
fastlane android test
```
Runs all the tests (unit tests and instrumented tests)

#### android unit_test
```bash
fastlane android unit_test
```
Runs unit tests only

#### android instrumentation_test
```bash
fastlane android instrumentation_test
```
Runs instrumented tests on connected device/emulator

#### android debug
```bash
fastlane android debug
```
Builds debug APK

#### android release
```bash
fastlane android release
```
Builds release APK (requires signing configuration)

#### android deploy
```bash
fastlane android deploy
```
Deploys the app to Google Play Store (internal track)

#### android analyze
```bash
fastlane android analyze
```
Runs static code analysis (detekt, lint, checkstyle, PMD)

#### android coverage
```bash
fastlane android coverage
```
Generates test coverage reports

#### android increment_version
```bash
fastlane android increment_version
```
Increments the version code

#### android beta
```bash
fastlane android beta
```
Deploys to Firebase App Distribution

#### android quality_check
```bash
fastlane android quality_check
```
Runs all quality checks (tests, analysis, coverage)

#### android prepare_release
```bash
fastlane android prepare_release
```
Prepares for release (version increment, quality checks, release build)

## Environment Variables

The following environment variables are required for various lanes:

```bash
# Signing Configuration
KEYSTORE_PATH="path/to/keystore.jks"
STORE_PASSWORD="store_password"
KEY_ALIAS="key_alias"
KEY_PASSWORD="key_password"

# Play Store
PLAY_STORE_CONFIG_JSON="path/to/play-store-config.json"

# Firebase
FIREBASE_APP_ID="your_firebase_app_id"
```

## CI/CD Integration

### GitHub Actions
```yaml
- name: Setup Ruby
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: '2.7'

- name: Install Fastlane
  run: gem install fastlane

- name: Run Tests
  run: fastlane android test

- name: Deploy to Play Store
  run: fastlane android deploy
  env:
    KEYSTORE_PATH: ${{ secrets.KEYSTORE_PATH }}
    STORE_PASSWORD: ${{ secrets.STORE_PASSWORD }}
    KEY_ALIAS: ${{ secrets.KEY_ALIAS }}
    KEY_PASSWORD: ${{ secrets.KEY_PASSWORD }}
    PLAY_STORE_CONFIG_JSON: ${{ secrets.PLAY_STORE_CONFIG_JSON }}
```

## Best Practices

1. **Secrets Management**
   - Never commit sensitive files (keystores, JSON keys)
   - Use environment variables for secrets
   - Use CI/CD secret management

2. **Version Control**
   - Commit Fastfile and Appfile
   - Include this README
   - Exclude sensitive files in .gitignore

3. **Testing**
   - Run tests before deployments
   - Include coverage checks
   - Run static analysis

4. **Deployment**
   - Use internal track first
   - Implement staged rollouts
   - Monitor crash reports

## Troubleshooting

### Common Issues

1. **Signing Issues**
   ```bash
   # Verify keystore
   keytool -list -v -keystore your_keystore.jks
   ```

2. **Play Store Upload Issues**
   - Verify JSON key permissions
   - Check version code increment
   - Validate release notes

3. **Test Failures**
   - Check device connection
   - Verify test dependencies
   - Review test logs

## Additional Resources

- [Fastlane Docs](https://docs.fastlane.tools)
- [Android Setup Guide](https://docs.fastlane.tools/getting-started/android/setup/)
- [Available Actions](https://docs.fastlane.tools/actions/)
- [CI Integration](https://docs.fastlane.tools/best-practices/continuous-integration/)
