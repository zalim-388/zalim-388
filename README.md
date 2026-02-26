name: 🐍 Generate Snake Animation

on:
  # Runs every 24 hours automatically
  schedule:
    - cron: "0 0 * * *"
  # Run manually from Actions tab
  workflow_dispatch:
  # Run on every push too
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate Snake SVG
        uses: Platane/snk@v3
        with:
          github_user_name: zalim-388
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
