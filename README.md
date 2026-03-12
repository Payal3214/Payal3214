name: 🟡 Generate Pac-Man Contribution Graph

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate Pac-Man SVG
        uses: bulldozer-official/3d-contrib@peglman
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          username: Payal3214
          type: pacman
          dark_scheme: true
          outputDir: dist
          filename: pacman-dark
          
      - name: Generate Pac-Man SVG (light)
        uses: bulldozer-official/3d-contrib@peglman
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          username: Payal3214
          type: pacman
          dark_scheme: false
          outputDir: dist
          filename: pacman

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
