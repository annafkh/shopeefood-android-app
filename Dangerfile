# frozen_string_literal: true

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Check for changes in crucial files
warn("Changes were made to AndroidManifest.xml") if git.modified_files.include? "app/src/main/AndroidManifest.xml"
warn("Changes were made to build.gradle") if git.modified_files.include? "app/build.gradle"

# Android Lint
android_lint.gradle_task = "app:lintDebug"
android_lint.report_file = "app/build/reports/lint-results-debug.xml"
android_lint.filtering = true
android_lint.lint(inline_mode: true)

# Detekt
kotlin_detekt.gradle_task = "detekt"
kotlin_detekt.report_file = "app/build/reports/detekt/detekt.xml"
kotlin_detekt.filtering = true

# JUnit tests
junit_tests_dir = "app/build/test-results/testDebugUnitTest"
Dir["#{junit_tests_dir}/*.xml"].each do |file_name|
  junit.parse file_name
  junit.report
end

# Checkstyle
checkstyle_format.base_path = Dir.pwd
checkstyle_format.report "app/build/reports/checkstyle/checkstyle.xml"

# PMD
pmd_report.report_file = "app/build/reports/pmd/pmd.xml"
pmd_report.report

# Coverage
coverage_files = Dir.glob("app/build/reports/coverage/**/*.xml").first
if coverage_files
  xcov.report(
    scheme: "Debug",
    workspace: "app/build/reports/coverage/debug/report.xml",
    minimum_coverage_percentage: 70.0
  )
end

# Check for TODOs/FIXMEs
warn("There are still some TODOs in the modified code") if git.modified_files.any? { |file| `grep -r TODO #{file}`.length > 0 }
warn("There are still some FIXMEs in the modified code") if git.modified_files.any? { |file| `grep -r FIXME #{file}`.length > 0 }

# Check for merge conflicts
git.commits.each do |c|
  if c.message =~ /^Merge branch/
    warn "Please rebase to get rid of the merge commits in this PR"
    break
  end
end

# Check commit message format
git.commits.each do |c|
  if c.message.lines.first.length > 72
    warn "Please keep the first line of commit messages under 72 characters"
  end
end

# Check for changes without tests
has_app_changes = !git.modified_files.grep(/src\/main\/java/).empty?
has_test_changes = !git.modified_files.grep(/src\/test\/java/).empty?
if has_app_changes && !has_test_changes
  warn("Tests were not updated", sticky: false)
end

# Check for documentation updates
has_doc_changes = !git.modified_files.grep(/\.md$/).empty?
if git.modified_files.any? { |file| file.end_with?(".java", ".kt") } && !has_doc_changes
  warn("Please update documentation for the changes")
end

# Check for version bump
version_changes = git.modified_files.include?("app/build.gradle") &&
  git.modified_files.include?("CHANGELOG.md")
if !version_changes && git.commits.any? { |c| c.message =~ /^feat:|^fix:/ }
  warn("Please include a version bump and update CHANGELOG.md")
end

# Check for package structure
if git.added_files.any? { |file| file =~ /src\/main\/java/ }
  warn("Please ensure new files follow the package structure")
end

# Check for resource naming
if git.modified_files.any? { |file| file =~ /res\/.*\.xml/ }
  warn("Please ensure resource names follow the naming convention")
end

# Spotless check
spotless_output = `./gradlew spotlessCheck`.strip
if spotless_output.include?("FAILURE")
  fail("Code style violations detected. Please run ./gradlew spotlessApply")
end

# Performance checks
warn("This PR might affect app performance") if git.modified_files.any? { |file| 
  file.include?("onDraw") || 
  file.include?("onMeasure") || 
  file.include?("onLayout")
}

# Security checks
warn("This PR might have security implications") if git.modified_files.any? { |file| 
  file.include?("WebView") || 
  file.include?("SharedPreferences") || 
  file.include?("ContentProvider")
}
