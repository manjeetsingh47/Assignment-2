name: Check for Broken links

on:
  push:
    branches: [ main ]
  schedule:
    - cron: '0 2 * * *'

jobs:
  lychee-link-check:
    runs-on: ubuntu-latest

    steps:
    - name: 📥 Checkout repository
      uses: actions/checkout@v4

    - name: 🔍 Run lychee link checker
      uses: lycheeverse/lychee-action@v1.8.0
      with:
        args: --verbose --no-progress './**/*.md' './**/*.html'

    - name: 📄 Upload lychee report
      uses: actions/upload-artifact@v4
      with:
        name: broken-link-report
        path: ./lychee/out.md
