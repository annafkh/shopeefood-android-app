source "https://rubygems.org"

# Fastlane and plugins
gem "fastlane"
gem "fastlane-plugin-firebase_app_distribution"
gem "fastlane-plugin-increment_version_code"
gem "fastlane-plugin-android_version_manager"
gem "fastlane-plugin-versioning_android"
gem "fastlane-plugin-changelog"
gem "fastlane-plugin-badge"
gem "fastlane-plugin-appicon"
gem "fastlane-plugin-ruby"
gem "fastlane-plugin-test_center"
gem "fastlane-plugin-automated_test_emulator_run"

# Code quality and documentation
gem "danger"
gem "danger-android_lint"
gem "danger-checkstyle_format"
gem "danger-junit"
gem "danger-kotlin_detekt"
gem "danger-todoist"
gem "danger-android_version_check"
gem "jazzy"
gem "yard"

# Build and deployment tools
gem "cocoapods"
gem "bundler"
gem "rake"
gem "rubocop"
gem "xcov"
gem "xcode-install"

# Testing and debugging
gem "pry"
gem "rspec"
gem "webmock"
gem "vcr"

# Version management
gem "semantic"
gem "version_sorter"

# Documentation generation
gem "redcarpet"
gem "rouge"

group :development do
  gem "debase"
  gem "ruby-debug-ide"
end

plugins_path = File.join(File.dirname(__FILE__), 'fastlane', 'Pluginfile')
eval_gemfile(plugins_path) if File.exist?(plugins_path)
